---
title: 300-longest-increasing-subsequence
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---


# problem
[300-longest-increasing-subsequence](https://leetcode.com/problems/longest-increasing-subsequence/#/description)
# solution
## solution 1 DP
转移矩阵先把问题转换成以这个点结束的最长递增子序列，在最后的时候遍历所有的节点，找到最长的长度
```cpp
    int lengthOfLIS(vector<int>& nums) {
        if (nums.empty() || nums.size() == 0)
            return 0;
        vector<int> lens( nums.size(),0 );//标记的是以这个位置结束的自增序列的长度;
        lens[0] = 1;
        for (int i = 1; i < nums.size(); i++)
        {
            //从0开始找比它大的位置;
            int bigger = 0;
            for (int j = 0 ; j < i; j ++)
                if (nums[i] > nums[j] && lens[j] > bigger)
                    bigger = lens[j];
            lens[i] = bigger + 1;//这里设置的比较巧妙，当i是递增序列中的第一个元素的时候，依然是成立的
        }
        //找到lens数组中的最大值;
        int maxLen = 0;
        for (int i = 0; i < lens.size(); i++)
            if (maxLen < lens[i])
                maxLen = lens[i];
        return maxLen;
    }
```
## solution2 lower bound

[longest_increasing_subsequence](https://algorithm.yuanbin.me/zh-hans/dynamic_programming/longest_increasing_subsequence.html)

```cpp
    int lengthOfLIS(vector<int>& nums) {
        if (nums.empty()) return 0;

        vector<int> lis;
        for (int i = 0; i < nums.size(); ++i) {
            vector<int>::iterator it = lower_bound(lis.begin(), lis.end(), nums[i]);
            if (it == lis.end()) {
                lis.push_back(nums[i]);
            } else {
                *it = nums[i];
            }
        }

        return lis.size();
    }
```

# reference

[c++的新特性](http://blog.csdn.net/wangshubo1989/article/details/50575008)