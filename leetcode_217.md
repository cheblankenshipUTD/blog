
## Leetcode: Contains Duplicate (217)
### Question
Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.


**Example 1:**

**Input:** nums = [1,2,3,1]
**Output:** true

**Example 2:**

**Input:** nums = [1,2,3,4]
**Output:** false

**Example 3:**

**Input:** nums = [1,1,1,3,3,4,3,2,4,2]
**Output:** true



#### Solution #1
In this solution, I used unordered_set to store the integers, and check if element is already inserted or not.
This approach will require additional O(n) space b/c of unordered_set.
Checking if the element is already in the set takes O(1).
Iterating thorugh each element will take O(n).

``` cpp
class Solution {
public:
	bool containsDuplicate(std::vector<int>&  nums) {
		std::unordered_set<int> numSet;
		for(int  n: nums)
		{
			std::unordered_set<int>::const_iterator it = numSet.find(n);
			if(it != numSet.end())
			{
				return true;
			}
			numSet.insert(n);
		}
		return false;
	}
};
```

#### Solution #2
Since the vector is pass by reference, we can use the original vector and sort it in order.
C++ STL sort: O(NlogN) time complexity.
Iterate through the vector and check adjacent element. If there is equal, then return true.
If loop ends without returning true, no duplicate in the vector; hence, return false.

``` cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int size = nums.size();
        if(size == 1)
            return false;
        std::sort(nums.begin(), nums.end());
		for(int i = 0; i < size - 1; i++)
		{
		    if(nums[i] == nums[i+1])
		    {
		        return true;
		    }
		}
		return false;
    }
};
```
