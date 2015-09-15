---
layout: post
title: "88 merge sorted array"
categories: leetcode
tags: array
---

>Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
>Note:
>You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

####1 我的思路

从nums1数组的m+n-1的位置开始排列，比较nums1 nums2元素的大小将大的放到nums1中。

{% highlight java linenos %}
public void merge(int[] nums1, int m, int[] nums2, int n) {
        if(n == 0) return;
        int i = m-1;
        int j = n-1;
        int k = (m+n-1);
        while(i >= 0 || j >= 0){
        	if(i < 0) nums1[k--] = nums2[j--];
        	else if(j < 0) nums1[k--] = nums1[i--];
        	else if(nums1[i] < nums2[j]) nums1[k--]=nums2[j--];
        	else nums1[k--]=nums1[i--];
        }

    }
{% endhighlight java %}

可以优化的部分是当nums2中的元素都移到nums1中后，就无需在进行任何操作。
这也是most votes中普遍的方法。
{% highlight java linenos %}
public void merge2(int[] nums1, int m, int[] nums2, int n) {
        if(n == 0) return;
        int i = m-1;
        int j = n-1;
        int k = (m+n-1);
        while(i >= 0 && j >= 0){
        	
            if(nums1[i] < nums2[j]) nums1[k--]=nums2[j--];
        	else nums1[k--]=nums1[i--];
        }
        while(j >= 0){
		nums1[k--]=nums1[j--];
        }
        
    }
{% endhighlight java %}

####2 most votes
基本同上。

在我做过的十几道题目中，很多都可以根据《算法》中的思路来解释。 