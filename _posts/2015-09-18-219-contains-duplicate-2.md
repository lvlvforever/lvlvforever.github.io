---
layout: post
title: "219 contains duplicate 2"
categories: leetcode
tags: array
---

>Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k.

####1  
最容易想到的方法是2层循环。不过提交显示超时了。
discuss中的most votes答案的思路是使用set结合滑动窗口。
{% highlight java linenos %}
public boolean containsNearbyDuplicate(int[] nums, int k) {
        if(nums == null) return false;
        Set<Integer> set = new HashSet<Integer>();
        for(int i = 0; i < nums.length; i++){
          if(i > k) set.remove(i-k-1);
          if(!set.add(nums[i])) return true;
        }
        return false;

     }
{% endhighlight java %}
以后贴一个自己实现的set，尽量不使用java本身特性解题。感觉这样有点投机取巧了。
