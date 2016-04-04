---
layout: post
title: Longest Substring Without Repeating Characters
category: Tech 
tags: 
  - CPP 
  - C 
  - leetcode
time: 2016.03.05 22:22:00
excerpt: NULL

---

##  题目
Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

## 答案
{% highlight cpp %}
class Solution{
public:
    int lengthOfLongestSubstring(string s){
        const int ASIC_MAX = 256;
        signed short last[ASIC_MAX]; // 记录字符串上次出现的问题
        int start = 0;              // 记录当前字符子串的起始位置
        int max_len = 0;
        
        fill(last, last + ASIC_MAX, -1); // 数组内容填充为-1

        for (int i = 0; i < s.length(); i++)
        {
            if (last[s[i]] >= start)
            {
                max_len = (i - start) > max_len ? i - start : max_len;
                start = last[s[i]] + 1;
            }
            last[s[i]] = i;
        }

		// 针对整个字符串没有重复的情况,需要做如下判断
        max_len = (int)s.length() - start > max_len ? (int)s.length() - start : max_len;
        return max_len;
    }
};
{% endhighlight %}

*本文参考：<https://leetcode.com/problems/longest-substring-without-repeating-characters/>*
