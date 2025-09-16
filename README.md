import sys

def main():
    graph = {}
    current_ranks = {}
    keys = {}

    for line in sys.stdin:
        line = line.strip()
        if not line:
            continue
        
        parts = line.split('\t')
        if len(parts) == 2:
            node, value = parts
            try:
                rank = float(value)
                current_ranks[node] = rank
            except ValueError:
                if node not in graph:
                    graph[node] = []
                neighbors = value.split(',')
                graph[node].extend(neighbors)
    
    nodes = sorted(graph.keys())
    keys = {}
    for idx, node in enumerate(nodes):
        keys[node] = idx
    
    n = len(nodes)
    
    M = [[0] * n for _ in range(n)]
    for node, neighbors in graph.items():
        if neighbors:
            transition_prob = 1.0 / len(neighbors)
            for neighbor in neighbors:
                M[keys[node]][keys[neighbor]] = transition_prob
    
    new_ranks = [0] * n
    for i in range(n):
        for j in range(n):
            node_i = nodes[i]  
            new_ranks[j] += M[i][j] * current_ranks.get(node_i, 0)
    
    for node, idx in keys.items():
        sys.stdout.write('%s\t%f\n' % (node, new_ranks[idx]))

if __name__ == '__main__':
    main()
def main():
    # For this implementation, reducer just passes through the results
    # since mapper does all the matrix calculation
    for line in sys.stdin:
        line = line.strip()
        if not line:
            continue
        sys.stdout.write(line + '\n')

if _name_ == '_main_':
    main()

reducer for pagerank

