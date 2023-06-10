### LintCode 920 · Meeting Rooms
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
    @return: if a person could attend all meetings
    """
    def can_attend_meetings(self, intervals: List[Interval]) -> bool:
        # TC: O(nlogn), SC: O(1)
        intervals.sort(key = lambda i: i.start)

        for i in range(1, len(intervals)):
            i1 = intervals[i]
            i2 = intervals[i-1]
            if i1.start < i2.end:
                return False
        return True