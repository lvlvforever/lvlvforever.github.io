---
layout: post
title: "169 marjority element"
categories: leetcode
tags: array
---

>Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

>You may assume that the array is non-empty and the majority element always exist in the array.

####1
我的思路是先排序，取中间元素，题目中说明了数组非空且肯定存在主元素，所以不用再验证了。
{% highlight java linenos %}
public int majorityElement(int[] nums) {
	quickSort(nums);
	return nums[nums.length / 2];
}
public void quickSort(int[] nums){
		if(nums == null || nums.length <  1) return;
		int hi = nums.length - 1;
		quickSort(nums,0,hi);
		
	}
	private void quickSort(int[] nums, int lo,int hi){
		if(lo >= hi) return;
		int j = partition(nums,lo,hi);
		quickSort(nums,lo,j-1);
		quickSort(nums,j+1,hi);
	}
	private int partition(int[] nums,int lo,int hi){
		int i = lo;
		int j = hi+1;
		int v = nums[lo];
		while(true){
			while(nums[++i] < v) if(i == hi) break;
			while(v < nums[--j]) if(j == lo) break;
			if(i >= j) break;
			swap(nums,i,j);
		}
		swap(nums,lo,j);
		return j;
	}
	 private void swap(int[] nums,int i, int j){
	 		if(i == j) return;
	 		if(nums[i] == nums[j]) return;
	    	nums[i] ^= nums[j];
	    	nums[j] ^= nums[i];
	    	nums[i] ^= nums[j];
	    }
{% endhighlight java %}

####2 most votes
《编程之美》2.3寻找发帖水王 中提到这个算法的解法:
> 如果每次删除两个不同的ID，那么在剩下的ID列表中，水王ID出现次数依然超过了一半。将问题转化为更小的问题。

{% highlight java linenos %}
public int majorityElement(int[] nums) {
		if(nums.length <= 1) return nums[0];
		int n = nums.length;
		int candidate = 0;
		int count = 0;
		for(int i = 0; i < n; i++){
			if(count == 0 ){
				candidate = nums[i];
				count = 1;
			}else{
				if(candidate == nums[i]) count++;
				else count--;
			}
		}
		return candidate;								
		
	}
{% endhighlight java %}