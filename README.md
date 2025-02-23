# DSA
138. COPY LIST WITH RANDOM POINTER [ LINKED LIST ]
![image](https://github.com/user-attachments/assets/583c9ec7-af29-47bd-8352-430fd5d18bb9)
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x, next=None, random=None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution(object):
    def copyRandomList(self, head):
        """
        :type head: Node
        :rtype: Node
        """
        #[[7,null],[13,0],[11,4],[10,2],[1,0]]

        if head==None:
            return None
        cur=head
        # inserting newnode in the middle of the main node
        while cur:
            newnode=Node(cur.val) # copied the first val and created a newnode that is 7
            newnode.next=cur.next # new node of 7 is pointing to cur node of nxt i.e 7 => is  13
            cur.next=newnode  # main node 7 is connecting to newnode 7 
            cur=newnode.next # then the main node is shifted
        # giving the pointer to the newnode
        cur=head
        while cur:
            if cur.random !=None:
                cur.next.random=cur.random.next #pointing the random points  
            cur= cur.next.next # moving  to the middle node
        # splitting the main node and newnode
        cur=head # main node i.e first node
        newhead=head.next # next of main node i.e newly created first node
        newcur=newhead # newcur is newnode i.e next of main node i.e newly created first node
        while cur:
            cur.next=newcur.next # just pointing the main node alone
            cur=cur.next # moving the main node alone
            if cur!=None:
                newcur.next=cur.next # pointing the newnode alone
                newcur=newcur.next # moving the newnode alone
        return newhead # returning the newnode 

```

169. MAJORITY ELEMENT:
The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

Example 1:

Input: nums = [3,2,3]
Output: 3
```python
nums.sort()
        l=0
        r=len(nums)-1
        return nums[(l+r)//2]
---
majority=nums[0]
        vote=0
        for i in range(len(nums)):
            if nums[i]==majority:
                vote+=1
            else:
                if vote<=0:
                    majority=nums[i]
                    vote+=1
                else:
                    vote-=1
        return majority
---
majority=nums[0]
        votes=0
        for i in range(len(nums)):
            if votes==0:
                majority=nums[i]
                votes+=1
            elif majority==nums[i]:
                votes+=1
            else:
                votes-=1
        return majority
```

74 SEARCH A 2D MATRIX
You are given an m x n integer matrix matrix with the following two properties:

Each row is sorted in non-decreasing order.
The first integer of each row is greater than the last integer of the previous row.
Given an integer target, return true if target is in matrix or false otherwise.
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true

APPROACH=>  i converted the 2d matrix as 1d as a asumption and used binary search for the finding the target, to find the i,j is dividing the value with col because the matrix has every thing in a col manner 
each row has col num eg: row =4 col=4 means 4 num in each row and the every row starts with the index mutiple of 4 which is col
```python
  row=len(matrix)
        col=len(matrix[0])
        l=0
        r=row*col-1
        while l<=r:
            mid=(l+r)//2
             i=mid//col #this is based on the nums in col and this is a formula
            j=mid%col
            if matrix[i][j]==target:
                return True
            elif matrix[i][j]<target:
                l=mid+1
            else:
                r=mid-1
        return False
```


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
31. NXT PERMUTATION :
The steps are the following:

=> Find the break-point, i: Break-point means the first index i from the back of the given array where arr[i] becomes smaller than arr[i+1].
For example, if the given array is {2,1,5,4,3,0,0}, the break-point will be index 1(0-based indexing). Here from the back of the array, index 1 is the first index where arr[1] i.e. 1 is smaller than arr[i+1] i.e. 5.
To find the break-point, using a loop we will traverse the array backward and store the index i where arr[i] is less than the value at index (i+1) i.e. arr[i+1].
=> If such a break-point does not exist i.e. if the array is sorted in decreasing order, the given permutation is the last one in the sorted order of all possible permutations. So, the next permutation must be the first i.e. the permutation in increasing order.
So, in this case, we will reverse the whole array and will return it as our answer.
=> If a break-point exists:
=> Find the smallest number i.e. > arr[i] and in the right half of index i(i.e. from index i+1 to n-1) and swap it with arr[i].
=> Reverse the entire right half(i.e. from index i+1 to n-1) of index i. And finally, return the array.
``` python
class Solution(object):
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        ind=-1 # break point
        n=len(nums) # size of the array.
        for i in range(n-2,-1,-1):
            if nums[i]<nums[i+1]: # index i is the break point
                ind=i
                break
        if ind== -1:  # If break point does not exist:
            nums.reverse() # reverse the whole array:
            return nums
        for i in range(n-1,ind,-1):  # Step 2: Find the next greater element
    #         and swap it with arr[ind]:
            if nums[i]>nums[ind]:
                nums[i],nums[ind]=nums[ind],nums[i]
                break
        nums[ind+1:]=reversed(nums[ind+1:]) # Step 3: reverse the right half:
        return nums
```
56 Merge Interval :
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```python

        intervals.sort()
        ans=[]
        for i in range(len(intervals)):
            if not ans  or intervals[i][0]> ans[-1][1]:
                ans.append(intervals[i])
            else:
                ans[-1][1]=max(intervals[i][1],ans[-1][1])
        return ans
```
88. MERGE SORTED ARRAY - EASY
You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.
nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
```python
last=m+n-1
        while m>0 and n>0:
            if nums1[m-1]>nums2[n-1]:
                nums1[last]=nums1[m-1]
                m-=1
            else:
                nums1[last]=nums2[n-1]
                n-=1
            last-=1 
        while n>0:
            nums1[last]=nums2[n-1]
            n,last=n-1,last-1
        return nums1
```
88.Merge sorted array
```python
for i in range(n):
            nums1[m+i] = nums2[i]
        return nums1.sort()
```
