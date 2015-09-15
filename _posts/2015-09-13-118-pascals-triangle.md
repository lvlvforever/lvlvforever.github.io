---
layout: post
title: "118 pascal's triangle"
categories: leetcode
tags: array
---

> Given numRows, generate the first numRows of Pascal's triangle.

> For example, given numRows = 5,
> Return

>[<br>
     [1],<br>
    [1,1],<br>
   [1,2,1],<br>
  [1,3,3,1],<br>
 [1,4,6,4,1]<br>
]<br>

####1
根据前一行生成下一行。
{% highlight java linenos %}
public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> pre = new ArrayList<Integer>();
		if(numRows <= 0) return result;
        pre.add(1);
        result.add(pre);
        int a,b;
        for(int i = 2; i <= numRows; i++){
        	List<Integer> eachLine = new ArrayList<Integer>();
        	for(int j = 1; j <= i; j++){
        		a = (j == 1) ? 0 : pre.get(j-2);
        		b = (j == i) ? 0 : pre.get(j-1);
        		eachLine.add(a+b);
        	}
        	result.add(eachLine);
        	pre = eachLine;
        }
        return result;
    }
{% endhighlight java %}

####2 most votes
by [rheaxu](https://leetcode.com/discuss/20606/my-concise-solution-in-java)
方法很巧妙，row始终是当前row,其中的row.add(0,1)用的很好，java doc对于这个方法的解释是
>void java.util.ArrayList.add(int index, Integer element)
>Inserts the specified element at the specified position in this list. Shifts the element currently at that 
>position (if any) and any subsequent elements to the right (adds one to their indices).
每次会在list最前面添加1，后续元素右移。
{% highlight java linenos %}
public class Solution {
public List<List<Integer>> generate(int numRows)
{
    List<List<Integer>> allrows = new ArrayList<List<Integer>>();
    ArrayList<Integer> row = new ArrayList<Integer>();
    for(int i=0;i<numRows;i++)
    {
        row.add(0, 1);
        for(int j=1;j<row.size()-1;j++)
            row.set(j, row.get(j)+row.get(j+1));
        allrows.add(new ArrayList<Integer>(row));
    }
    return allrows;

}
{% endhighlight java %}