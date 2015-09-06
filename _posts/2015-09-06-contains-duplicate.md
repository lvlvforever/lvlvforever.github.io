---
layout: post
title: "217 contains duplicate"
categories: leetcode
tags: array
---

>Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

{% highlight java linenos %}
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        
    }
}
{% endhighlight java %}

####1
排序，然后遍历查找。
{% highlight java linenos %}
public boolean containsDuplicate(int[] nums) {
     	if(nums == null || nums.length <= 1) return false;
     	heapSort(nums);  
     	for(int i = 0; i < nums.length-1;i++){
     		if(nums[i] == nums[i+1]) return true;
     	}
     	return false;
    }
    private void heapSort(int[] nums){
    	int n = nums.length - 1;
    	for(int i=n/2; i>=0;i--){
    		sink(nums,i,n);
    	}
    	while(n > 0){
    		swap(nums,0,n--);
    		sink(nums,0,n);
    	}
    }
    private void sink(int[] nums,int i,int n){
    	int tmp;
    	while((tmp = 2 * i + 1) <= n){
    		int j = tmp;
    		if(j < n && less(nums,j,j+1)) j++;
    		if(!less(nums,i,j)) break;
    		swap(nums,i,j);
    		i = j;
    	}
    }
    private boolean less(int[] a, int i, int j){
		return a[i] < a[j];
	}

    private void swap(int[] nums,int i, int j){
    	nums[i] ^= nums[j];
    	nums[j] ^= nums[i];
    	nums[i] ^= nums[j];
    }
{% endhighlight java %}

####2 most votes
以下的代码都用到了java的本身的语言特性。set集中不存在重复元素。

- by [riskycheng](https://leetcode.com/discuss/user/riskycheng)

{% highlight java linenos %}
public  boolean containsDuplicate(int[] nums) {
         Set<Integer> set = new HashSet<Integer>();
         for(int i : nums)
             if(!set.add(i))// if there is same
                 return true; 
         return false;
     }
{% endhighlight java %}

- by [jmnarloch](https://leetcode.com/discuss/user/jmnarloch)

{% highlight java linenos %}
public boolean containsDuplicate(int[] nums) {

    final Set<Integer> distinct = new HashSet<Integer>();
    for(int num : nums) {
        if(distinct.contains(num)) {
            return true;
        }
        distinct.add(num);
    }
    return false;
}
{% endhighlight java %}