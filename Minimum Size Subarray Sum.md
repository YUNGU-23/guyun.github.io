### LC 209. Minimum Size Subarray Sum

class Solution:
def minSubArrayLen(self, target: int, nums: List[int]) -> int:
    l, sum = 0, 0                                   # use sliding window method
    res = float("inf")                              # define an infinite number

    for r in range(len(nums)):                      # r = [0,1,...len(nums)-1)
        sum += nums[r]                              # to sum up
        while sum >= target:                        # find the interval that >= target 
            res = min(r - l + 1, res)               # find the interval's minimun length
            sum -= nums[l]                          # sum subtract the first number
            l += 1                                  # "l" pointer move one step to the right
    return 0 if res == float("inf") else res

### LC 904. Fruit Into Baskets

class Solution:
def totalFruit(self, fruits: List[int]) -> int:   
    max_len = float("-inf")                                 # if max use "-inf" else "inf"
    dic = {}                                                # define a dictionary to store the charcter and its amount
    l, sum = 0, 0                                           # define the "l" pointer and the sum
    for r in range(len(fruits)):                            # 
        if fruits[r] not in dic:                            # add fruits[r] into dic
            dic[fruits[r]] = 1                              # if dic doesn't have fruits[r], add fruits[r]'s amount to 1
        else:                                               # if dic has fruits[r], add fruits[r]'s amount by 1
            dic[fruits[r]] += 1
        while len(dic) > 2:                                 # if dic has more than 2 elements, move the "l" pointer to right
            dic[fruits[l]] -= 1
            if dic[fruits[l]] == 0:                         # if dic has no fruits[l], delete fruits[l]
                del dic[fruits[l]]
            l += 1                                          # "l" pointer move one step to right
        max_len = max(r - l + 1, max_len)                   # get the maximum value
    return 0 if max_len == float("-inf") else max_len       # return the result
 
### LC 76. Minimum Window Substring -- Hard

class Solution:                                                     # the code does not work
def minWindow(self, s: str, t: str) -> str:
    if t == "": return ""                                       

    countT, window = {}, {}                                         # define two dictionary to count the characters of T
    for c in t:                                                     # traverse the characters in t
        countT[c] = 1 + countT.get(c, 0)                            # store the number of characters of T 
    
    have, need = 0, len(countT)                                     # define two conter to store the needed characters number, need for countT, have for window
    res, resLen = [-1, -1], float("infinity")                       # define float("infinity") to minimun length
    l = 0                                                           # define the "l" pointer
    for r in range(len(s)):                                         # define the "r" pointer
        c = s[r]                                                    #
        window[c] = l + window.get(c, 0)                            # store the number of characters of T in s

        if c in countT and window[c] == countT[c]:                  # the character in s is also in countT and its number in window equal to that in countT
            have += 1                                               # the counter "have" add 1

        while have == need:                                         # when the number of charcters in window is equal to that in countT
            # update our result
            if (r - l + 1) < resLen:                                # judge the minimum length  
                res = [l, r]                                        # adjust the result's interval
                resLen = (r - l + 1)                                # update the result's length
            # pop from the left of our window
            window[s[l]] -= 1                                       # pop the left charcter in s
            if s[l] in countT and window[s[l]] < countT[s[l]]:      # if the left pointer pops s[l] in countT and the number of s[l] in window is less than that in countT
                have -= 1                                           # the counter "have" minus one
            l += 1                                                  # "l" pointer move right by one step
    l, r = res                                                      
    return s[l:r+1] if resLen != float("infinity") else ""