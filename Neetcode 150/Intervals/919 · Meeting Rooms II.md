### Lintcode 919 · Meeting Rooms II
from typing import (
    List,
)
from lintcode import (
    Interval,
)

"""
Definition of Interval:
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    """
    @param intervals: an array of meeting time intervals
    @return: the minimum number of conference rooms required
    """
    def min_meeting_rooms(self, intervals: List[Interval]) -> int:
        # Write your code here
        if len(intervals) == 0: return 0
        if len(intervals) == 1: return 1
        start = sorted([i.start for i in intervals]) # [0,5,15]
        end = sorted([i.end for i in intervals])    # [10,20,30]
        s, e, count, res = 0, 0, 0, 0
        while s < len(intervals):
            if start[s] < end[e]:
                s += 1
                count += 1
            else:
                e += 1
                count -= 1
            res = max(res, count)
        return res