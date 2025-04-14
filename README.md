# DSA
1248 COUNT NICE SUBARRAY
Input: nums = [1,1,2,1,1], k = 3
Output: 2
Explanation: The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].
```PYTHON
class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        res=0
        odd=0
        l,m=0,0
        for r in range(len(nums)):
            if nums[r]%2!=0:
                odd+=1
            
            while odd >k:
                if nums[l]%2!=0:
                    odd-=1
                l+=1
                m=l
            if odd==k:
                while nums[m] %2 == 0: #unitl finds odd number
                    m+=1
                res+=(m-l)+1
        return res

```
424 LONGEST REPEATING CHAR REPLACEMENT:
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
Example 2:
```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count={}
        res=0
        l=0
        for r in range(len(s)):
            count[s[r]]=1+count.get(s[r],0)
            
            while (r-l+1) - max(count.values()) >k: #len of arr - maxfreq
                count[s[l]]-= 1
                l+=1
            res=max(res,r-l+1)
        return res


```
930 BINARY SUBARRAY WITH K:
```python
def numSubarraysWithSum(self, nums: List[int], goal: int) -> int:
        def helper(x):
            if x<0:return 0
            res,l,cur=0,0,0
            for r in range(len(nums)):
                cur+=nums[r]
                while cur>x:
                    cur-=nums[l]
                    l+=1
                res+=(r-l+1)
            return res
        



        return helper(goal)-helper(goal-1)

```

904 FRUITS INTO BASKET:
Input: fruits = [1,2,1]
Output: 3
Explanation: We can pick from all 3 trees.


Example 2:

Input: fruits = [0,1,2,2]
Output: 3
Explanation: We can pick from trees [1,2,2].
If we had started at the first tree, we would only pick from trees [0,1].


239. MAXIMUM SLIDING WINDOW
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation:

```python
def totalFruit(self, fruits: List[int]) -> int:
        l=max_one=0
        basket=collections.defaultdict(int)
        for r in range(len(fruits)):
            basket[fruits[r]]+=1
            
            while len(basket)>2:
                basket[fruits[l]]-=1
                if  basket[fruits[l]]==0:
                    del  basket[fruits[l]]
                l+=1
            max_one=max(max_one,r-l+1)
        return max_one
```


 ```python
# st=[]
    
        # for i in range(len(nums)-k+1):
        #     max_num=nums[0]
        #     for j in range(i,i+k):
        #         max_num=max(max_num,nums[j])
        #     st.append(max_num)
        # return st
        output=[]
        q=collections.deque()
        l=r=0
        while r<len(nums):
            #pop the smaller values from deque
            while q and nums[q[-1]] < nums[r]:
                q.pop()
            q.append(r)
            # remove left val from window
            if q[0]<l:
                q.popleft()
            if (r-l+1)>=k:
                output.append(nums[q[0]])
                l+=1
            r+=1
        return output
```
402. REMOVING K DIGIT:
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.

```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        
        st=[]
        for i in num:
            while st and k>0 and st[-1] > i:
                st.pop()
                k-=1
            st.append(i)
        while k>0 and st: # if all the num is small then k is still > 0 pop the num in st
            st.pop()
            k-=1
        res=''.join(st).lstrip('0')
        return res if res else '0'
        

```
42.TRAPPING RAIN WATER:




![image](https://github.com/user-attachments/assets/bc0b8c67-9980-4990-8b4b-26177c102ed1)



Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        #BRUTE FORCE METHOD
        # count=0
        # if not height:
        #     return 0
        # for i in range(len(height)):
            
            
        #     leftmax = max(height[:i+1])  # Max height on the left
        #     rightmax = max(height[i:])   # Max height on the right
        #     if height[i]<leftmax and height[i]< rightmax:
        #         count +=min(leftmax, rightmax) - int(height[i])
              
        
        # return count


        #OPTIMIZED CODE USING TWO POINTER 
        l=0
        r=len(height)-1
        leftmax=rightmax=count=0
        while l<r:
            if height[l] <= height[r]:
                if height[l] >= leftmax:
                    leftmax = height[l]
                else:
                    count+= leftmax - height[l]
                l+= 1
            else:
                if height[r] <= height[l]:
                    if height[r] >= rightmax:
                        rightmax = height[r]
                    else:
                        count+= rightmax - height[r]
                    r-= 1
        return count
```

496. NEXT GREATER ELEMENT:
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- ```python
  class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        st=[]
        next_great={}
        for i in reversed(nums2):
            while st and st[-1] <= i:
                st.pop()
            next_great[i]=st[-1] if st else -1
            st.append(i)
        return [next_great[i] for i in nums1]
  ```
Find XOR of numbers from L to R.
Input: 
L = 4, R = 8 
Output:
8 
Explanation:
4 ^ 5 ^ 6 ^ 7 ^ 8 = 8
```python
   def findXOR(self, l, r):
        # Code here
        # ans=l
        # for i in range(l+1,r+1):
        #     ans^=i
        # return ans
        def XOR(n):
            if n % 4 == 0:
                return n
            elif n % 4 == 1:
                return 1
            elif n % 4 == 2:
                return n + 1
            else:
                return 0
        
        # XOR from l to r = XOR(1 to r) ^ XOR(1 to l-1)
        return XOR(r) ^ XOR(l-1)
        
       
# Number	XOR Result So Far
# 1	1
# 2	1 ^ 2 = 3
# 3	3 ^ 3 = 0
# 4	0 ^ 4 = 4
# 5	4 ^ 5 = 1
# 6	1 ^ 6 = 7
# 7	7 ^ 7 = 0
# 8	0 ^ 8 = 8
# 9	8 ^ 9 = 1


# n % 4	XOR(1 to n)
# 0	n
# 1	1
# 2	n+1
# 3	0
                

```
46. PERMUTATION:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```PYTHON
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res=[]
        #base case
        if len(nums)==1:
            return [nums[:]] # or [nums.copy()]
        for i in range(len(nums)):
            n=nums.pop(0)
            perms=self.permute(nums)
            for perm in perms:
                perm.append(n)
            res.extend(perms)
            nums.append(n)
        return res
```

131. PALINDROME PARTITIONING:
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
![WhatsApp Image 2025-03-02 at 19 41 20_a4d6c3ea](https://github.com/user-attachments/assets/7653645b-5126-456f-ab53-4c0e178b067e)


```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        res=[]
        part=[]
        def dfs(i):
            if i>=len(s):
                res.append(part.copy())
                return
            for j in range(i,len(s)):
                if isPali(s,i,j):
                    part.append(s[i:j+1])
                    dfs(j+1)
                    part.pop()
        def isPali(s,l,r):
            while l<r:
                if s[l]!=s[r]:
                    return False
                l,r=l+1,r-1
            return True
       
    
        dfs(0)
        return res
```
90 SUBSET 2 AND 78 SUBSET 1:

90. has no duplicate
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]

78=> it may have duplicate ...

Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

![WhatsApp Image 2025-03-01 at 18 18 29_e42c84f7](https://github.com/user-attachments/assets/fe97b31e-d9d9-40d3-9dfd-675a40a8407b)
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res=[]
        def back(i,cur):
            if i>=len(nums):
                res.append(cur.copy())
                return
            cur.append(nums[i])
            back(i+1,cur)
            cur.pop()
            back(i+1,cur)
        back(0,[])
        return sorted(res)

```
```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        res=[]
        nums.sort()
        def back(i,cur):
            if i>=len(nums):
                res.append(cur.copy())
                return
            cur.append(nums[i])
            back(i+1,cur)
            cur.pop()
            while i+1 < len(nums) and  nums[i] == nums[i+1]:
                i+=1
            back(i+1,cur)
        back(0,[])
        return res
```


40 COMBINATION SUM 2:
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
![WhatsApp Image 2025-03-01 at 17 50 38_9ae79fa4](https://github.com/user-attachments/assets/eed4e56d-d78f-45c8-9412-195bbf79f295)
```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        # candidates.sort()
        # res = []

        # def backtrack(cur, pos, target):
        #     if target == 0:
        #         res.append(cur.copy())
        #         return
        #     for i in range(pos, len(candidates)):
        #         if i > pos and candidates[i] == candidates[i - 1]:  # ✅ Skip duplicates
        #             continue
        #         if candidates[i] > target:  
        #             break  
        #         cur.append(candidates[i])
        #         backtrack(cur, i + 1, target - candidates[i])  # ✅ Move to next index (no reuse)
        #         cur.pop()  # Backtrack

        # backtrack([], 0, target)
        # return res
        candidates.sort()
        res=[]
        def backtrack(i,cur,total):
            if total==target:
                res.append(cur.copy())
                return
            if total>target or i>=len(candidates):
                return 
            cur.append(candidates[i])
            backtrack(i+1,cur,total+candidates[i])
            cur.pop()
            # i+1<len(candiates) if the array like [1,1,1,1]
            while i+1<len(candidates) and candidates[i]==candidates[i+1]:
                i+=1
            backtrack(i+1,cur,total)
        backtrack(0,[],0)
        return res

```

39 COMBINATION SUM 1 :
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
![WhatsApp Image 2025-03-01 at 17 50 37_e3d22b65](https://github.com/user-attachments/assets/c8de97da-e326-4de9-b7ec-71c0f7c21ded)


```PYTHON
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        # res=[]
        # def backtrack(start,target,path):
        #     if target==0:
        #         res.append(list(path))
        #         return
        #     for i in range(start,len(candidates)):
        #         if candidates[i]>target:
        #             continue
        #         path.append(candidates[i])
        #         backtrack(i,target-candidates[i],path)
        #         path.pop()
        

        # backtrack(0,target,[])
        # return res
        res=[]
        def backtrack(i,cur,total):
            if total==target:
                res.append(cur.copy())
                return
            if i>=len(candidates) or total>target:
                return
            cur.append(candidates[i]) 
            backtrack(i,cur,total+candidates[i])
            cur.pop()
            backtrack(i+1,cur, total)
        backtrack(0,[],0)
        return res

```
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
