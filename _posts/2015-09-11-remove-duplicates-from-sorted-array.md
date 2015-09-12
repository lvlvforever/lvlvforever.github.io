---
layout: post
title: "26 remove duplicates from sorted array"
categories: leetcode 
tags: array
---

> Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

> Do not allocate extra space for another array, you must do this in place with constant memory.

> For example,
> Given input array nums = [1,1,2],

> Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
> It doesn't matter what you leave beyond the new length.

####1
使用一个新指针idx,指向当前有效的数组，使用一个遍历指针i,利用数组已经有序的条件，将nums[i]与nums[idx]比较，
相同则继续遍历，不相同则更新idx指针，同时将nums[i]保存到nums[idx]。
{% highlight java linenos %}
public int removeDuplicates(int[] nums) {
     	   if(nums == null || nums.length == 0) return 0;
     	   int n = nums.length;
     	   int idx = 0;
     	   for(int i = 1; i < n; i++){
     	   		if(nums[i] != nums[idx]){
     	   			nums[++idx] = nums[i]; 
     	   		}
     	   }
     	   return idx+1;
    }
{% endhighlight java %}

####2 most votes 
方法类似。