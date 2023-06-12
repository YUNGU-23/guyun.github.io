### LC 704: Binary Search

class Solution:
def search(self, nums: List[int], target: int) -> int:
    l, r = 0, len(nums) - 1
    while l <= r:                       # Define a left-closed right-closed interval
        middle = l + (r - l)//2         # here is "//", if "/ " type will be float
        if nums[middle] < target:       # target is in the (mid: r) interval
            l = middle + 1              # because of nums[mid] < target, So the "l" pointer moves to "mid+1"
        elif nums[middle] > target:     # target is in the [l: mid) interval
            r = middle - 1              # because of nums[mid] >target, So the "r" pointer moves to "mid-1"
        else:                           # nums[mid] = target
            return middle
    return -1

### LC 35: Search Insert Position

class Solution:
def searchInsert(self, nums: List[int], target: int) -> int:
    l, r = 0, len(nums)-1
    while l <= r:                    # Define a left-closed right-closed interval
        mid = l + (r - l) // 2       # define the middle pointer
        if nums[mid] < target:       # target is in the (mid: r) interval
            l = mid + 1              # because of nums[mid] < target, So the "l" pointer moves to "mid+1"
        elif nums[mid] > target:     # target is in the [l: mid) interval
            r = mid - 1              # because of nums[mid] >target, So the "r" pointer moves to "mid-1"
        else:                        # nums[mid] = target
            return mid
    return l                         # if target is not in nums, l = r = mid --> l = mid + 1 --> return l

### LC 34. Find First and Last Position of Element in Sorted Array

class Solution:
def searchRange(self, nums: List[int], target: int) -> List[int]:
    left = self.binSearch(nums, target, True)       # load the binSearch method and look for the left most value
    right = self.binSearch(nums, target, False)     # load the binSearch method and look for the right most value
    return [left, right]

def binSearch(self, nums, target, leftBias):        # define a new method, because it will operate two times
    l, r = 0, len(nums) - 1                         # define the left and right pointer
    i = -1                                          # set a new variable
    while l <= r:
        mid = l + (r - l) // 2
        if nums[mid] < target:
            l = mid + 1
        elif nums[mid] > target:
            r = mid - 1
        else:                                       # nums[mid] = target
            i = mid                                 
            if leftBias:                            # look for the left most value
                r = mid - 1                         # update the pointer
            else:                                   # look for the right most value
                l = mid + 1                         # update the pointer
    return i

### LC 69. Sqrt(x)

class Solution:
def mySqrt(self, x: int) -> int:
    l, r = 0, x                     # use two pointers method
    while l <= r:                   # define a left-closed right-closed interval
        mid = l + (r - l) // 2      # define the middle
        if mid * mid > x:           # target(x) in the left interval [l: mid * mid)
            r = mid - 1             # "r" pointer move to "mid - 1"
        else:                       # target(x) in the right interval [mid * mid: r]
            l = mid + 1             # "l" pointer move to "mid + 1"
    return r                        # when l = r = mid, mid * mid will be greater than x, so will operate r = mid - 1

### LC 367. Valid Perfect Square

class Solution:
def isPerfectSquare(self, num: int) -> bool:
    l, r = 1, num                   # use two pointers method
    while l <= r:                   # define a left-closed right-closed interval
        mid = l + (r - l) // 2      # define the middle
        if mid * mid < num:         # num in the right interval
            l = mid + 1
        elif mid * mid > num:       # num in the left interval
            r = mid - 1
        else:                       # mid * mid = num
            return True             
    return False