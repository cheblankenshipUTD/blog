
## Leetcode: Contains Duplicate (217)
### Question
Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

 

Example 1:

Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
Example 2:

Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
Example 3:

Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
 

Constraints:

n == nums.length
1 <= n <= 104
0 <= nums[i] <= n
All the numbers of nums are unique.
 

Follow up: Could you implement a solution using only O(1) extra space complexity and O(n) runtime complexity?


#### Solution #1
In this solution, I used unordered_set to store the integers, and check if element is already inserted or not.
This approach will require additional O(n) space b/c of unordered_set.
Checking if the element is already in the set takes O(1).
Iterating thorugh each element will take O(n).

``` cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int length = nums.size();
        sort(nums.begin(), nums.end());
        if(nums[0] != 0) return 0;
        if(nums[length-1] != length) return length;
        for(int i = 1; i < length; i++)
        {
            if(nums[i] - nums[i-1] != 1)
            {
                return (nums[i] + nums[i-1]) / 2;
            }
        }
        return -1;
    }
};
```