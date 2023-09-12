## This is my first blog post
Let's see the first coding day for leetcode. Now I try to solve two problems in my 150 daily chanllenge.

Let's add something for my code
 ```tsql
 SELECT *
 FROM sys.tables
 WHERE [name] = 'SomeTable'
 ```
I want to solve the first problem which is 88. Merge Sorted Array

The description is here: 
You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

 

Example 1:

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
Example 2:

Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].
Example 3:

Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.

now we can see what changed in here. Here is my solution!

Code Explanation:
Purpose: This code provides a solution to merge two sorted arrays, nums1 and nums2. The resulting merged array is stored in-place in nums1.
In-place Modification: The code modifies the nums1 array in-place, making efficient use of space.
Backward Iteration: The solution adopts a reverse approach, filling nums1 from the end. It compares the last elements of both nums1 (from its valid elements) and nums2 and places the larger of the two at the end of nums1.
Choosing Elements: The conditional checks (if nums1[m-1] >= nums2[n-1] and m>0:) decide whether to pick the current element from nums1 or nums2 for the next position in the merged array.
Pointer Updates: After placing an element from either nums1 or nums2 into its correct position, the respective pointer (m or n) is decremented.

 ```python3
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """

        while n > 0:
            if nums1[m-1] >= nums2[n-1] and m>0:
                nums1[m+n-1] = nums1[m-1]
                m-=1
            else:
                nums1[m+n-1] = nums2[n-1]
                n-=1
 ```

And my thought was:   
I adopted a reverse iteration approach to merge the two arrays. By comparing the end elements of both arrays and filling nums1 from its end, I ensured efficient and in-place merging. The pointers m and n were instrumental in keeping track of the current elements being compared and determining the placement of elements in the merged array.


Next we can go to the second problem I solved today. 

26. Remove Duplicates from Sorted Array
The description is here:
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.
Custom Judge:

The judge will test your solution with the following code:

int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
If all assertions pass, then your solution will be accepted.

 

Example 1:

Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
Example 2:

Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Here is my code to solve this problem:

Code Explanation:
Double Pointer Technique: The code uses the double pointer technique (often referred to as the two-pointer technique). One pointer (denoted by ans) is used to keep track of the position in the array where the next unique element should be placed. The other pointer (the loop variable i) iterates through the array.
Iteration: The loop starts from the second element of the array (since the first element is always unique) and checks if the current element is different from the previous element.
Unique Element Found: If a unique element is found (i.e., nums[i] is not equal to nums[i-1]), it's placed at the position indicated by the ans pointer, and then the ans pointer is incremented.
Return Value: The function returns the length of the array after duplicates have been removed (denoted by ans).

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        #use double pointer ans and j to solve this problem
        """
        as we can see, the initial array is already sorted.
        So we just need to know if the first pointer is equal to second pointer.
        """
        ans = 1
        for i in range(1, len(nums)):
            if nums[i] != nums[i-1]:
                nums[ans] = nums[i]
                ans += 1
        return ans

```

I've utilized the two-pointer technique, where one pointer ('slow') lags behind the other ('fast'). The 'slow' pointer indicates where the next unique element should be placed, while the 'fast' pointer traverses the array.


"The method employs the two-pointer technique. Here, one pointer (referred to as the 'slow' pointer) tracks the position for placing the next unique element, while the other ('fast' pointer) iterates through the array. As the sorted nature of the array ensures that duplicates are adjacent, we can efficiently identify and skip duplicates, placing only unique elements at the position indicated by the 'slow' pointer."

