---
layout: post
title: " 27 remove element"
categories: leetcode
tags: array
---

>Given an array and a value, remove all instances of that value in place and return the new length.

>The order of elements can be changed. It doesn't matter what you leave beyond the new length.

#### 
我的思路是遍历数组，遇到nums[i]==val 则交换最右侧元素与当前元素，同时i--。
{% highlight java linenos %}
 public int removeElement(int[] nums, int val) {
        int n = nums.length;
        int hi = n - 1;
        for(int i = 0; i <= hi; i++){
        	if(nums[i] == val){
        		swap(nums,i,hi--);
        		i--;
        	}
        }
        return hi+1;
    }
	 private void swap(int[] nums,int i, int j){
	 		if(i == j) return;
	    	nums[i] ^= nums[j];
	    	nums[j] ^= nums[i];
	    	nums[i] ^= nums[j];
	    }
{% endhighlight java %}

#### most votes
by[rantos22](https://leetcode.com/discuss/56609/c-4ms-very-elegant)
这个真的是很简洁，标题是very elegant！
{% highlight java linenos %}
int removeElement(vector<int>& nums, int val) 
{
    size_t idx(0);
    for (const int num : nums)    
    {
        if ( num != val)
            nums[idx++] = num;
    }

    return idx;
}
{% endhighlight java %}

java版本:
{% highlight java linenos %}
public int removeElement(int[] nums, int val) {
    	if(nums == null || nums.length == 0) return;
    	int n = nums.length;
    	int idx = 0;
    	for(int i = 0; i < n; i++){
    		if(nums[i] != val){
    			nums[idx++]=nums[i];
    		}
    	}
    	return idx;

    }
{% endhighlight java %}