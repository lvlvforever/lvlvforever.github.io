---
layout: post
title: "229 marjority element 2"
categories: leetcode
tags: array
---

>Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times. The algorithm should run in linear time and in O(1) space.

####1
这道题很容易想到 marjority element 那道题。这类题称为Boyer-Moore Majority Vote Element Algorithm。我觉得和上一篇的一样，寻找大于n/2元素时，关键是从数组中去掉2个不同的元素，结论不变。
寻找大于n/3元素时，关键是从数组中去掉3个不同的元素时，结论不变。
{% highlight java linenos %}
public List<Integer> majorityElement(int[] nums) {
     	if(nums == null) return null;
     	List<Integer> list = new ArrayList<Integer>();
     	
     	int candidate1 = 0;
     	int candidate2 = 0;
     	int count1 = 0;
     	int  count2 = 0;
     	for(int i = 0; i < nums.length; i++){
     		int tmp = nums[i];

     		if(count1 == 0 && count2 == 0){
     			candidate1 = tmp;
     			count1 = 1;
     		}else if(count1 == 0 && count2 != 0){
     			if(tmp != candidate2) 
     				{
     					candidate1 = tmp;
     					count1++;
     				}
     			else count2++;
     		}else if(count2 == 0 && count1 != 0){
     			if(tmp != candidate1) {
     				candidate2 = tmp;
     				count2++;
     			}
     			else count1++;
     		}else if(tmp == candidate1){
     			count1++;
     		}else if(tmp == candidate2){
     			count2++;
     		}else{
     			count1--;
     			count2--;
     		}

     	}
     	int count = 0;
     	if(count1 != 0){

     		for(int i = 0; i < nums.length; i++){
     			if(candidate1 == nums[i]) count++;
     		}
     		if(count > nums.length/3)
     			list.add(candidate1);
     	}
     	if(count2 != 0){
     		count = 0;
     		for(int i = 0; i < nums.length; i++){
     			if(candidate2 == nums[i]) count++;
     		}
     		if(count > nums.length/3)
     			list.add(candidate2);
     	}
     	return list;

    }
{% endhighlight java %}
代码写的罗嗦了一些，根据2中的python代码写了下面简洁一些的代码。仅是关键代码。
{% highlight java linenos %}
		int candidate1 = 0;
     	int candidate2 = 1;
     	int count1 = 0;
     	int  count2 = 0;
     	for(int i = 0; i < nums.length; i++){
     		int tmp = nums[i];

     		 if(tmp == candidate1){
     			count1++;
     		}else if(tmp == candidate2){
     			count2++;
     		}else if(count1 == 0){
                    candidate1 = tmp;
                    count1 = 1;
            }else if(count2 == 0){
                    candidate2 = tmp;
                    count2 = 1;
            }else{
     			count1--;
     			count2--;
     		}

     	}
{% endhighlight java %}

####2 most votes
by [chungyushao](https://leetcode.com/discuss/43248/boyer-moore-majority-vote-algorithm-and-my-elaboration)
{% highlight python linenos %}
class Solution:
# @param {integer[]} nums
# @return {integer[]}
def majorityElement(self, nums):
    if not nums:
        return []
    count1, count2, candidate1, candidate2 = 0, 0, 0, 1
    for n in nums:
        if n == candidate1:
            count1 += 1
        elif n == candidate2:
            count2 += 1
        elif count1 == 0:
            candidate1, count1 = n, 1
        elif count2 == 0:
            candidate2, count2 = n, 1
        else:
            count1, count2 = count1 - 1, count2 - 1
    return [n for n in (candidate1, candidate2)
                    if nums.count(n) > len(nums) // 3]
{% endhighlight python %}