# 1. Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = \[2,7,11,15\], target = 9 Output: \[0,1\] Output: Because nums\[0\] + nums\[1\] == 9, we return \[0, 1\].

Example 2:

Input: nums = \[3,2,4\], target = 6 Output: \[1,2\]

Example 3:

Input: nums = \[3,3\], target = 6 Output: \[0,1\]

题解：

```text
class Solution{
    public:
    vector<int> twoSum(vector<int>& nums,int target){
        int i,j;
        for(i = 0;i<nums.size()-1;i++){
            for(j =i+1;j<nums.size();j++){
                if(nums[i]+nums[j] == target)
                return{i,j};
            }
        }
        return{i,j};
    };
};
```

leetcode第一題 沒什麼難度 兩層循環 ,時間複雜度（n2n^2n2 ）。

兩個指針，一個指針從第一個數開始，一個從第二個數開始，第一個不動，第二個走遍整個數組，沒有找到，第一個指針到第二個數，第二個數從第三個數開始，找到爲止，返回這組數。

