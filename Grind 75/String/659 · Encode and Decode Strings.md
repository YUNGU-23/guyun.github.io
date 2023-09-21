#### Lintcode: 659 · Encode and Decode Strings
class Solution:
    def encode(self, strs):
        # lint -> 4#lint
        res = ''
        for s in strs:
            res += str(len(s)) + '#' + s
        return res

    def decode(self, str):
        # 4#lint -> lint
        res, i = [], 0
        while i < len(str):
            j = i
            while str[j] != '#':
                j += 1
            resLen = int(str[i:j])
            res.append(str[j+1:j+1+resLen])
            i = j + 1 + resLen
        return res