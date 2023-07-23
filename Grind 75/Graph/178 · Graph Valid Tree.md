### LintCode: 178 · Graph Valid Tree
from typing import (
    List,
)

class Solution:
    """
    @param n: An integer
    @param edges: a list of undirected edges
    @return: true if it's a valid tree, or false
    """
    def valid_tree(self, n: int, edges: List[List[int]]) -> bool:
        # use DFS, TC: O(e + v), SC: O(e + v)
        if not n: 
            return True
        # find adj
        adj = {i:[] for i in range(n)}
        for n1, n2 in edges:
            adj[n1].append(n2)
            adj[n2].append(n1)
        # def 
        visited = set()
        def dfs(i, pre):
            if i in visited: 
                return False
            visited.add(i)
            # traversal i's adj
            for j in adj[i]:
                # skip pre node
                if j == pre:
                    continue
                if not dfs(j, i):
                    return False
            return True
        
        # dfs only detect if have cycle or loop, we also need check visited length
        return dfs(0, -1) and len(visited) == n