# DSA
75 SORT COLORS
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
``` Python 
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        l=0
        r=len(nums)-1
        
        i=0
        while i<=r: #after r we don't wnat to check beacuse it will be sorted 
            if nums[i]==0:
                nums[i],nums[l]=nums[l],nums[i] 
                i+=1
                l+=1
            elif nums[i]==2:
                nums[i],nums[r]=nums[r],nums[i]
                r-=1
            else:
                i+=1

            
```
658 FIND K CLOSEST ELEMENT
Input: arr = [1,2,3,4,5], k = 4, x = 3

Output: [1,2,3,4]
```python
class Solution(object):
    def findClosestElements(self, arr, k, x):
        """
        :type arr: List[int]
        :type k: int
        :type x: int
        :rtype: List[int]
        """
        left =0
        right=len(arr)-k
        while left<right:
            mid=(left+right)//2
            if x-arr[mid]>arr[mid+k]-x:
                left=left+1
            else:
                right=mid
        return arr[left:left+k]

            
```
209 Minimum subsize array
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
``` python
class Solution(object):
    def minSubArrayLen(self, target, nums):
       
        l=0
        r=0
        subsum=0
        min_arr=[]
        while r<len(nums):
            subsum+=nums[r]
            while subsum>=target:
                min_arr.append(r-l+1)
                subsum-=nums[l]
                l+=1
            r+=1
        return 0 if len(min_arr)==0 else min(min_arr)
```
53. MAX SUBARRAY
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
```python
Approach
removing the negative value after adding the cur_sum of each iteration if the cur_sum in not <0 then we will find the max of cur_sum and max_sub

class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        max_sub=nums[0]
        cur_sum=0
        for i in nums:
            if cur_sum<0:
                cur_sum=0
            cur_sum+=i
            max_sub=max(max_sub,cur_sum)
        return  max_sub

```
