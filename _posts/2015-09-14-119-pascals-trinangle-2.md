---
layout: post
title: "119 pascal's trinangle 2"
categories: leetcode 
tags: array
---

> Given an index k, return the kth row of the Pascal's triangle.

> For example, given k = 3,
> Return [1,3,3,1].

> Note:
> Could you optimize your algorithm to use only O(k) extra space?

####1
思路是根据前一行的值迭代计算下一行的值。空间复杂度是O(k)。
1 3 3 1 -> 1 4 6 4 1
具体内部实现可以使用list,java.util.ArrayList.add(int index, Integer element)的方法在增加元素后，将后续元素依次右移。
也可以使用数组。
注意当rowIndex = 0时，输出是[1]。
{% highlight java linenos %}
public List<Integer> getRow(int rowIndex) {
        ArrayList<Integer> row = new ArrayList<Integer>();
        for(int i = 0; i <= rowIndex; i++){
        	row.add(0,1);
        	for(int j = 1; j < row.size() -1; j++){
        		row.set(j,row.get(j)+row.get(j+1));
        	}
        }
        return row;
    }
    public List<Integer> getRow2(int rowIndex) {
    	Integer[] row = new Integer[rowIndex+1];
    	for(int i = rowIndex; i >= 0; i--){
    		row[i] = 1;
    		for(int j = i+1; j <= rowIndex-1; j++){
    			row[j] = row[j]+row[j+1];
    		}
    	}
    	return Arrays.asList(row);

    }
    public List<Integer> getRow3(int rowIndex) {
    	rowIndex++;
    	Integer[] row = new Integer[rowIndex];
    	for(int i = rowIndex-1; i >= 0; i--){
    		row[i] = 1;
    		for(int j = i+1; j <= rowIndex-2; j++){
    			row[j] = row[j]+row[j+1];
    		}
    	}
    	return Arrays.asList(row);

    }
{% endhighlight java %}

####2 most votes
基本上都是这个思路。
