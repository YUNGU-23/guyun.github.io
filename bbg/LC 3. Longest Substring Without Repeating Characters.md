### LC 3. Longest Substring Without Repeating Characters
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        # set, sliding window, l = 0, traversal r, and check if s[r] in set, if is remove s[l] and update l pointer, and records the max length to res 
        # TC: O(n), SC: O(n)
        strSet = set()
        l = 0
        res = 0
        for r in range(len(s)):
            while s[r] in strSet:
                strSet.remove(s[l])
                l += 1
            strSet.add(s[r])
            res = max(res, r - l + 1)
        return res