---
layout: post
title: "80 remove duplicates from sorted array 2"
categories: leetcode 
tags: array
---

> Follow up for "Remove Duplicates":
> What if duplicates are allowed at most twice?

> For example,
> Given sorted array nums = [1,1,1,2,2,3],

> Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. 
> It doesn't matter what you leave beyond the new length.

####1
idx 是新数组的指针，i是nums数组的遍历指针。使用flag表示当前重复的元素个数。
如果nums[i] != nums[idx],更新idx,将nums[i]存到nums[idx],同时置flag为0。
如果nums[i] == nums[idx]且flag < 1，说明当前重复元素为0个，可以更新idx,将nums[i]存到
nums[idx]，同时flag加1。
如果题目变为最多允许出现k次，将flag < 1改为flag < k-1即可。
{% highlight java linenos %}
 public int removeDuplicates(int[] nums) {
     	   if(nums == null || nums.length == 0) return 0;
     	   int n = nums.length;
     	   int idx = 0;
           int flag = 0;
           int tol
     	   for(int i = 1; i < n; i++){
     	   		if(nums[i] != nums[idx]){
                     nums[++idx] = nums[i]; 
                     flag = 0;
               }else if(nums[i] == nums[idx] && flag < 1){
                    nums[++idx] = nums[i]; 
                    flag++;
                }
     	   }
     	   return idx+1;
    }
{% endhighlight java %}

####2 most votes

by [StefanPochmann](https://leetcode.com/discuss/42348/3-6-easy-lines-c-java-python-ruby)

思路是将当前遍历元素与新数组的倒数第二个元素比较，只有n大于此元素才添加新元素。
太精炼了。也可以扩展到最多允许出现k次的情况。
{% highlight java linenos %}
public int removeDuplicates(int[] nums) {
    int i = 0;
    for (int n : nums)
        if (i < 2 || n > nums[i-2])
            nums[i++] = n;
    return i;
}
{% endhighlight java %}