### LC 59. Spiral Matrix II

class Solution:
def generateMatrix(self, n: int) -> List[List[int]]:
    nums = [[0] * n for _ in range(n)]                  # [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
    startx, starty, loop, mid = 0, 0, n//2, n//2        # define variables
    count = 1                                           # filled element

    for offset in range(1, loop + 1):                   # Number of cycles
        # right
        for i in range(startx, n-offset):               # i = [0:n-1) --> i = [0,1]
            nums[startx][i] = count                     # [0,0] = 1, [0,1] = 2
            count += 1                                  # count = 3
        # down
        for i in range(startx, n - offset):             # i = [0:n-1) --> i = [0,1]
            nums[i][n - offset] = count                 # [0,2] = 3, [1,2] = 4
            count += 1                                  # count = 5
        # left
        for i in range(n - offset, starty, -1):         # i = [n-1,0) --> i = [2,1]
            nums[n - offset][i] = count                 # [2,2] = 5, [2,1] = 6
            count += 1                                  # count = 7
        # up
        for i in range(n - offset, startx, -1):         # i = [n-1,0) --> i = [2,1]
            nums[i][starty] = count                     # [2,0] = 7, [1,0] = 8
            count += 1
        startx += 1                                     # prepare for the next loop
        starty += 1
    
    if n % 2:                                           # judege whether n is even, if not:
        nums[mid][mid] = count
    return nums               

### LC54. Spiral Matrix

class Solution:
def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
    res = []                                        
    left, right = 0, len(matrix[0])                 # define the left and right pointers
    top, bottom = 0, len(matrix)                    # define the top and bottom pointers

    while left < right and top < bottom:
        # get every i in the top row
        for i in range(left,right):
            res.append(matrix[top][i])
        top += 1
        # get every i in the right column
        for i in range(top,bottom):
            res.append(matrix[i][right-1])
        right -= 1
        
        if not (left < right and top < bottom):
            break
        
        # get every i in the bottom row
        for i in range(right-1, left-1,-1):
            res.append(matrix[bottom-1][i])
        bottom -= 1
        # get every i in the left column
        for i in range(bottom-1, top-1,-1):
            res.append(matrix[i][left])
        left += 1
    return res