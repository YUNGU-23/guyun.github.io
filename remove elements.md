### LC 27. Remove Element

class Solution:
def removeElement(self, nums: List[int], val: int) -> int:
    slow, fast = 0, 0                   # use slow and fast pointers method
    while fast < len(nums):             # fast = [0,1,2,3]
        if nums[fast] != val:           
            nums[slow] = nums[fast]     
            slow += 1
        fast += 1
    return slow

### LC 26. Remove Duplicates from Sorted Array

class Solution:
def removeDuplicates(self, nums: List[int]) -> int:
    l, r = 0, 0                     # use two pointers method
    while r < len(nums):            # r = [0,1,...len(nums)-1]
        if nums[l] != nums[r]:
            l += 1                  # "l" pointer move forward first
            nums[l] = nums[r]       # give nums[r]'s value to nums[l]
        r += 1                      # "r" pointer move forward 
    return l + 1                    # "l" starts from 0, so the length should be "l + 1"

### LC 283. Move Zeroes

class Solution:
def moveZeroes(self, nums: List[int]) -> None:
    """
    Do not return anything, modify nums in-place instead.
    """
    l, r = 0, 0                                     # use two pointers method
    while r < len(nums):                            # r = [0,1,...len(nums)-1]
        if nums[r] != 0:                            
            nums[l], nums[r] = nums[r], nums[l]     # when nums[r] != 0, exchange the value of nums[l] and nums[r]
            l += 1                                  # "l" pointer move forward
        r += 1                                      # "r" pointer move forward
    return nums

### LC 844. Backspace String Compare

class Solution:
def backspaceCompare(self, s: str, t: str) -> bool:
    res1, res2 = "", ""             # define empty string
    for i in s:                     # organize the characters in "s"
        if i != "#":                
            res1 += i               # when i != "#", store the character into res1
        else:
            res1 = res1[: -1]       # when i = "#", remove the last character
    
    for i in t:                     # organize the characters in "t"
        if i != "#":
            res2 += i               # when i != "#", store the character into res1
        else:
            res2 = res2[: -1]       # when i = "#", remove the last character
    
    return res1 == res2             # judge whether res1 is equal to res2, if equal return True, else return False
