---
layout: post
title: " 228 summary ranges"
categories: leetcode
tags: array
---

> Given a sorted integer array without duplicates, return the summary of its ranges.

>For example, given [0,1,2,4,5,7], return ["0->2","4->5","7"].

####1
先看代码:
{% highlight java linenos %}
 public List<String> summaryRanges(int[] nums) {
		List<String> list  = new ArrayList<String>();
     	if(nums == null || nums.length == 0) return list;
     	int n = nums.length;
     	int start = 0;
     	int end = 0;
     	boolean isSearch = false;
     	for(int i = 0; i < n-1; i++){
     		if(isSearch == false) start = i;
     		if(nums[i+1] == nums[i] + 1){
     			isSearch = true;
     		}
     		else  {
     			end = i;
     			isSearch = false;
     			String tmp = generate(nums,start,end);
     			list.add(tmp);
     		}
     	}
     	if(isSearch == false){
     		String tmp = generate(nums,n-1,n-1);
     		list.add(tmp);
     	}else{
     		String tmp = generate(nums,start,n-1);
     		list.add(tmp);
     	}
     	return list;

    }
    private String generate(int[] nums,int left,int right){
    	if(left == right)
    		return nums[left]+"";
    	else{
    		return nums[left]+"->"+nums[right];
    	}
    }
{% endhighlight java %}

我是这么想的:使用start end两个变量标识连续元素的起点终点，使用isSearch表示当前位置是起点还是在连续元素之间。
初始化start=end=0,遍历元素，当isSearch==false时，说明开始了寻找新的一段连续元素，start置为当前的i。如果i+1的元素和i的元素相差1，则isSearch置为true,表示当前处于连续元素之间，当i+1和i的元素差值不为1，则将end置为i,isSearch置为false,表示这一段连续元素的起点是start,终点是end。注意一下最后的元素，当isSearch为false时，表示最后一个元素单独成为一段，当isSearch为true时，表示最后一个元素是以start为首的连续字符的最后一个元素。
(我发现我说半天还是说不清楚一个问题，想说的详细点却说的很啰嗦，争取多写，多表达自己的想法)

####2 most votes
这个基本上就是这个思路。

