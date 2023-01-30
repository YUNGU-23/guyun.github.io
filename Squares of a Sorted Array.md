### LC 977. Squares of a Sorted Array

class Solution:
def sortedSquares(self, nums: List[int]) -> List[int]:
    res = []                                            # define empty list
    l, r = 0, len(nums) - 1                             # use left and right pointers method
    while l <= r:
        if nums[l] * nums[l] > nums[r] * nums[r]:       # find the largest square number on left and right side
            res.append(nums[l] * nums[l])               # add the largest square number to res
            l += 1                                      # "l" pointer move one step to the right
        else:                                           # find the largest square number on left and right side
            res.append(nums[r] * nums[r])               # add the largest square number to res
            r -= 1                                      # "r" pointer move one step to the left
    return res[::-1]                                    # reverse the res, "-1" means the step is "-1"