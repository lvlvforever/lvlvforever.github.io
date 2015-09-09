---
layout: post
title: "189 rotate array"
categories: leetcode
tags: array
---

> Rotate an array of n elements to the right by k steps.

> For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

**Note:**
>Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

**Hint:**
>Could you do it in-place with O(1) extra space?

####
题目的意思很明确，将数组循环移k位，不难得知，k%n是实际的移动位数。<br>
比如<br>
1 2 3 4 5 6 7 8 <br>
n = 8 k = 3<br>
移位的次序依次为<br>
1->4 4->7 7->2 2->5 5->8 8->3 3->6<br>
刚好一趟完成，当时觉得对于所有的n k值均是一趟完成，后来想到<br>
1 2 3 4 5 6<br>
n = 6 k = 2<br>
则明显不是一趟完成，于是首先想到的是一位一位的移动。
{% highlight java linenos %}
 public void move(int[] nums,int k){
		int n = nums.length;
		k = k % n;
		for(int i = 0; i < k; i++){
			int tmp = nums[n-1];
			for(int j = n-1; j > 0; j--){
				swap(nums,j,j-1);		
			}
			nums[0] = tmp;
		}
	}
{% endhighlight java %}
提交上去time exceeded。一位一位的移动肯定是慢成狗。
仔细比较移动前和移动后的序列，之后的序列相当于是把后K个元素放到前面的，所以可以用下面的方法。
使用了O(k)个多余的空间。
{% highlight java linenos %}
 public void rotate(int[] nums, int k) {
    if(nums == null || nums.length == 1) return; 
        int n = nums.length;
        int realK = k%n;
        int last = n - realK;
        int[] aux = new int[k];
        for(int i = last; i < n; i++){
        	aux[i-last] = nums[i];
        }
        for(int i = last-1;i >= 0; i--){
        	swap(nums,i,i+realK);
        }
        for(int i=0; i < realK; i++){
        	nums[i] = aux[i];
        }
    }
    private void swap(int[] a ,int i, int j){
	int tmp = a[i];
	a[i] = a[j];
	a[j] = tmp;
}
{% endhighlight java %}
后来查到对于长度为n的数组移k位，根据数论的知识(我也不知道)，
需要移动gcd(n,k)趟，每次移动n/gcd(n,k)。
比如<br>
1 2 3 4 5 6<br>
n = 6, k = 2<br>
移动2趟，每次移动3个元素
1: 1->3 3->5 5->1
2: 2->4 4->6 6->2
所以有了下面的代码
{% highlight java linenos %}
public void rotate(int[] nums, int k) {
        if(nums == null || nums.length <= 1) return;
        int n = nums.length;
        int round = GCD(n,k);
        int count = n / round;

        for(int i = 0; i < round; i++){
        	int tmp1 = nums[i];
        	int p = i;
        	for(int j = 0; j < count ; j++){
        		int next = (p+k)%n;
        		int tmp2 = nums[next];
        		nums[next] = tmp1;
        		tmp1 = tmp2;
        		p = next;
        	}
        }

    }
    private int GCD(int p,int q){
    	if(q == 0) return p;
    	int r = p % q;
    	return GCD(q,r);
    }
{% endhighlight java %}

#### most votes 
by [monaziyi](https://leetcode.com/discuss/26148/3-line-using-reverse)
三次逆序即可。
1 2 3 4 5 6<br>
n = 6,k = 2<br>
第一次逆序:6 5 4 3 2 1 <br>
第二次逆序:5 6 4 3 2 1 <br>
第三次逆序:5 6 1 2 3 4 <br>
{% highlight java linenos %}
 private void reverse(int[] nums,int lo,int hi){
    	for(;lo < hi;lo++,hi--){
    		swap(nums,lo,hi);
    	}
    }

    public void rotateArray(int[] nums,int k){
    	int n = nums.length;
    	k = k % n;
    	reverse(nums,0,n-1);
    	reverse(nums,0,k-1);
    	reverse(nums,k,n-1);
    }
{% endhighlight java %}
