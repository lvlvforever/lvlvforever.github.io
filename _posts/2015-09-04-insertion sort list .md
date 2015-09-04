---
layout: post
title: 147 insertion sort list
categories: leetcode
tags: sort
---
>Sort a linked list using insertion sort.
>/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode insertionSortList(ListNode head) {
        
    }
}

####1 
插入排序的链表实现
{% highlight java linenos %}
public ListNode insertionSortList(ListNode head){
		if(head == null || head.next == null) return head;
		ListNode dummyHead = new ListNode(0);
		while(head != null){
			ListNode pre = dummyHead;
			while(pre.next != null && pre.next.val < head.val){
				pre = pre.next;
			}
			ListNode tmp = head.next;
			head.next = pre.next;
			pre.next = head;
			head = tmp;
		}
		return dummyHead.next;
	}
{% endhighlight java %}

####2 most votes 
一样。