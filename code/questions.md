- 手写transformer
- 寻找两个有序数组的中位数
  
        n = len(nums1)
        m = len(nums2)
        m1 = 0
        m2 = 0
        i = 0
        j = 0
  
        for count in range((m+n)//2+1):
            m2 = m1
            if i<n and j<m:
                if nums1[i]>nums2[j]:
                    m1 = nums2[j]
                    j += 1
                else:
                    m1 = nums1[i]
                    i += 1
            elif i<n:
                m1 = nums1[i]
                i += 1
            elif j<m:
                m1 = nums2[j]
                j += 1

        if (m+n)%2==0:
            return (m1+m2)/2
        else: return m1

        return 0
  
- 在底部高度不规则的正方形水池中，判断水面高度为t时是否能从左上角游到右下角，寻找最小的t以满足能游到右下角
- 找出字符串中最长的不含重复字符的子串长度
  
      class Solution:
        def lengthOfLongestSubstring(self, s: str) -> int:
            count = 0
            for i in range(len(s)):
                lst = []
                for j in range(i,len(s)):
                    if s[j] not in lst:
                        lst.append(s[j])
                        if count<len(lst):
                            count = len(lst)
                    else: break
            return count
- 计算岛屿数量
- 最长回文字串
  
        class Solution:
          def expend(self, s, left, right):
              while left>=0 and right<len(s) and s[left]==s[right]:
                  left -= 1
                  right += 1
              return left + 1, right -1 
      
      
          def longestPalindrome(self, s: str) -> str:
              start = 0
              end = 0
              for i in range(len(s)):
                  l1, r1 = self.expend(s, i, i)
                  l2, r2 = self.expend(s, i, i+1)
                  if r1-l1>end-start:
                      start, end = l1, r1
                  if r2-l2>end-start:
                      start, end = l2, r2
              return s[start: end+1]
- 数组中的第K个最大元素
- 小偷知道每家有多少钱，但偷了一家之后，不能偷挨着的两家，否则立刻会报警。输入一个列表，记录每家有多少钱，输出小偷能偷到的最多的钱

      class Solution:
        def rob(self, nums: List[int]) -> int:
            if len(nums) == 0: return 0
            if len(nums) <=2: return max(nums)
            if len(nums) ==3: return max(nums[0]+nums[2], nums[1])
    
            dp = [nums[0],  max(nums[0], nums[1]), max(nums[0]+nums[2], nums[1])]
            for i in range(3, len(nums)):
                dp.append(
                    max(
                        dp[i-1], dp[i-2]+ nums[i], dp[i-3]+ nums[i]
                    )
                )
            return dp[-1]
  
- leetcode 20， 有效的括号

      class Solution(object):
          def isValid(self, s):
              """
              :type s: str
              :rtype: bool
              """
              if len(s)%2!=0 or s[0] not in ["(", "[", "{"]:
                  return False
              
              lst = []
              for i in s:
                  if i in ["(", "[", "{"] or len(lst) == 0:
                      lst.append(i)
                  else:
                      if lst[-1]+i in ["()","[]","{}"]:
                          lst.pop()
                      else:
                          return False
                      
              if len(lst)>0:
                  return False
      
              return True


