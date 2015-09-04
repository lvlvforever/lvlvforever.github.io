---
layout: post
title: 179 lagest number
categories: leetcode
tags: sort
---
>Given a list of non negative integers, arrange them such that they form the largest number.

>For example, given [3, 30, 34, 5, 9], the largest formed number is 9534330.

>Note: The result may be very large, so you need to return a string instead of an integer.

####1
我的想法是排序，然后按顺序输出即可。关键在于如何排定两个元素的顺序。可以这么做：
比如 86 76 ，那么就比较7686 8676的大小即可。
代码里实现了快排，我尽量会少用java的语言特性，加强自己的基本功训练。
{% highlight java linenos %}
public String largestNumber(int[] nums){
		if(nums == null || nums.length == 0) return "0";
		int allZero = 0;
		for(int i = 0; i < nums.length; i++){
			if(nums[i]==0)
			allZero++;
		}
		if(allZero == nums.length) return "0";
		quickSort(nums,0,nums.length-1);
		StringBuilder sb = new StringBuilder();
		for(int i = 0; i < nums.length; i++){
			sb.append(nums[i]);
		}
		return sb.toString();
	}
	private void quickSort(int[] nums,int lo,int hi){
		if(nums == null || nums.length < 1) return;
		if(lo >= hi) return;
		int j = partition(nums,lo,hi);
		quickSort(nums,lo,j-1);
		quickSort(nums,j+1,hi);
	}
	 private void swap(int[] nums,int i, int j){
	 		if(i == j) return;
	 		if(nums[i] == nums[j]) return;
	    	nums[i] ^= nums[j];
	    	nums[j] ^= nums[i];
	    	nums[i] ^= nums[j];
	    }
	 private boolean bigger(int[] nums, int i, int j){
	    	if(nums[i] == 0) return false;
	    	if(nums[j] == 0) return true;
	    	int idigits  = 0;
	    	int jdigits  = 0;
	    	long a = nums[i];
	    	long b = nums[j];
	    	while(a != 0){
	    		a = a / 10;
	    		idigits++;
	    	}
	    	while(b != 0){
	    		b = b / 10;
	    		jdigits++;
	    	}
	    	 a = nums[i];
	    	 b = nums[j];
	    	for(int k = 0;  k < jdigits;  k++){
	    		a *= 10;
	    	}
			for(int  k = 0;  k < idigits;  k++){
	    		b *= 10;
	    	}
	    	return (a+nums[j]) > (b+nums[i]);

	    }
	    
	  private int partition(int[] nums,int lo, int hi){
	  	int i = lo;
	  	int j = hi+1;
	  	while(true){
	  		while(bigger(nums,++i,lo)) if(i == hi) break;
	  		while(bigger(nums,lo,--j)) if(j == lo) break;
	  		if(i >= j) break;
	  		swap(nums,i,j); 
	  	}
	  	swap(nums,lo,j);
	  	return j;
	  }
{% endhighlight java %}

####2 most votes
思路也和我的一样，排序，排序的比较方法，输出。
{% highlight java linenos %}
public  String largestNumber(int[] num) {
    if(num==null || num.length==0)
        return "";
    String[] Snum = new String[num.length];
    for(int i=0;i<num.length;i++)
        Snum[i] = num[i]+"";

    Comparator<String> comp = new Comparator<String>(){
        @Override
        public int compare(String str1, String str2){
            String s1 = str1+str2;
            String s2 = str2+str1;
            return s1.compareTo(s2);
        }
    };

    Arrays.sort(Snum,comp);
    if(Snum[Snum.length-1].charAt(0)=='0')
        return "0";

    StringBuilder sb = new StringBuilder();

    for(String s: Snum)
        sb.insert(0, s);

    return sb.toString();

}
{% endhighlight java %}