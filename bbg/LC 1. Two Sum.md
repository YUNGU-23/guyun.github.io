#### LC 1. Two Sum
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # use hashMap, enumerate, TC: O(n), SC: O(n)
        hashMap = {}    # value: index pair
        for i, v in enumerate(nums):
            if target - v in hashMap:
                return [hashMap[target - v], i]
            hashMap[v] = i
        return []