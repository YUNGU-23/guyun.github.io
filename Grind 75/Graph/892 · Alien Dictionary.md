### LintCode: 892 · Alien Dictionary
from typing import (
    List,
)

class Solution:
    def alien_order(self, words: List[str]) -> str:
        # use postorder dfs, TC: O(w + c), SC: O(w + c)
        # find c:set() pair
        adj = {c:set() for w in words for c in w}
        # add Alien dict to this map
        for i in range(len(words) - 1):
            w1, w2 = words[i], words[i + 1]
            minLen = min(len(w1), len(w2))
            # corner case 
            if len(w1) > len(w2) and w1[:minLen] == w2[:minLen]:
                return ''
            for j in range(minLen):
                if w1[j] != w2[j]:
                    adj[w1[j]].add(w2[j])
                    break
        
        visit = {}  # {c:False/True} pair, False = visited, True = current path
        res = []

        # use postorder dfs
        def dfs(c):
            if c in visit:
                return visit[c]
            visit[c] =True
            for nei in adj[c]:
                if dfs(nei):
                    return True     # have loop
            visit[c] = False
            res.append(c)

        for c in adj:
            if dfs(c):
                return ""
        res.reverse()
        return "".join(res)