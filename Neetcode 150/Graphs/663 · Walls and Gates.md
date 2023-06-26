### Lintcode: 663 · Walls and Gates
from typing import (
    List,
)

class Solution:
    """
    @param rooms: m x n 2D grid
    @return: nothing
    """
    def walls_and_gates(self, rooms: List[List[int]]):
        # use bfs
        rows, cols = len(rooms), len(rooms[0])
        q = collections.deque()
        visited = set()

        def addRoom(r, c):
            if (r < 0 or c < 0 or r == rows or c == cols or (r, c) in visited or rooms[r][c] == -1):
                return 
            q.append([r, c])
            visited.add((r, c))

        for r in range(rows):
            for c in range(cols):
                if rooms[r][c] == 0:
                    q.append([r, c])
                    visited.add((r, c))
        dist = 0
        while q:
            for i in range(len(q)):
                r, c = q.popleft()
                rooms[r][c] = dist
                addRoom(r + 1, c)
                addRoom(r - 1, c)
                addRoom(r, c + 1)
                addRoom(r, c - 1)
            dist += 1
