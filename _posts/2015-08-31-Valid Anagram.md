---
layout: post
title: 242 Valid Anagram
categories: leetcode
tags: sort
---
### Valid Anagram 
> 	Given two strings s and t, write a function to determine if t is an anagram of s. <br>
	For example,<br>
	s = "anagram", t = "nagaram", return true.<br>
	s = "rat", t = "car", return false.<br>
	Note:<br>
	You may assume the string contains only lowercase alphabets.
题目的意思理解了anagram这个单词就理解了，这个词是“易位构词”的意思，其实就是指两个字符串的组成字母是否完全一致。
题目中给的两个例子也很明显。
####1 
我的思路是先排序，然后挨个比较。自己实现的快排。
{% highlight java linenos %}
public class Solution {
    public boolean isAnagram(String s, String t) {
        if(s == null || t == null){
			return false;
		}
		if(s.length() != t.length()){
			return false;
		}
		char[] schar = s.toCharArray();
		char[] tchar = t.toCharArray();
		quickSort(schar);
		quickSort(tchar);
		for(int i = 0; i < s.length();i++){
			if(schar[i] != tchar[i]) return false;
		}
		return true;
	}
	public static void quickSort(char[] a){
		int n = a.length;
		quickSort(a,0,n-1);
	}
	private static void quickSort(char[] a,int lo,int hi){
		if(lo >= hi) return;
		int j = partition(a,lo,hi);
		quickSort(a,lo,j-1);
		quickSort(a,j+1,hi);
	}
	private static int partition(char[] a,int lo,int hi){
		int i = lo;
		int j = hi+1;
		while(true){
			while(less(a,++i,lo)) if(i == hi) break;
			while(less(a,lo,--j)) if(j == lo) break;
			if(i >= j) break;
			swap(a,i,j);
		}
		swap(a,lo,j);
		return j;
	}
	private static void swap(char[] a,int i,int j){
		char tmp = a[i];
		a[i] = a[j];
		a[j] = tmp;
	}
	private static boolean less(char[] a, int i,int j){
		return a[i] < a[j];
	}
}
{% endhighlight java %}

####2 leetcode discuss
{% highlight java linenos %}
public static boolean isValidAnagram(String s,String t){
		if(s.length() != t.length()) return false;
		int[] count = new int[26];
		for(int i = 0; i < s.length(); i++){
			count[s.charAt(i) - 'a']++;
			count[t.charAt(i) - 'a']--;
		}
		for(int i = 0; i < count.length; i++){
			if(count[i] != 0) return false;
		}
		return true;
	}
{% endhighlight java %}