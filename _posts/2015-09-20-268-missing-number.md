---
layout: post
title: "268 missing number"
categories: leetcode
tags: array
---

>Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

>For example,
>Given nums = [0, 1, 3] return 2.

>Note:
>Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

####1
计算0..n的总和，减去nums中元素的总和即为缺失的元素。
{% highlight java linenos %}
public int missingNumber(int[] nums) {
         if(nums == null || nums.length == 0) return 0;
        int n = nums.length;
        int sum = n*(n+1)/2;
        int total = 0;
        for(int i = 0; i < nums.length; i++){
        	total += nums[i];
        }
        return sum - total;
    }
{% endhighlight java %}
运行时间我测了三次，代码不变，分别是424ms,448ms,404ms。
这种方法有可能产生溢出，改进如下:
by [yifangchen](https://leetcode.com/discuss/53778/java-solution-o-1-space-and-o-n-in-time)

{% highlight java linenos %}
public class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int basic;
        int sum = 0;
        if(n%2 == 0) basic =n/2;   //according to the formula n*(n+1)/2, if n is even, add n/2 for n+1 times, otherwise, add (n+1)/2 for n times;
        else basic = (n+1)/2;
        for(int i=0;i<n;++i)
        {
            sum = sum + basic - nums[i];
        }
        if(n%2 == 0) sum += basic;
        return sum;
    }
}
{% endhighlight java %}

####2 most votes
by [CodingKing](https://leetcode.com/discuss/53802/c-solution-using-bit-manipulation)
思路是使用了异或的两个性质。

1. 自己与自己异或为0
2. 满足交换律 

元素index 是0...n-1，元素则为从0..n中去掉一个数字，这时添加上n，则除了缺少的元素其他元素在index和数组中共计均出现了2次。
{% highlight c++ linenos %}
class Solution {
    public:
    int missingNumber(vector<int>& nums){
         int result = nums.size();
         int i=0;

         for(int num:nums){
            result ^= num;
            result ^= i;
            i++;
          }

        return result;
        }
    }
{% endhighlight c++ %}
