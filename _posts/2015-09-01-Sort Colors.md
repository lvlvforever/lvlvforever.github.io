---
layout: post
title: 75 Sort Colors
categories: leetcode
tags: sort
---
>Given an array with n objects colored red, white or blue, sort them so that objects of the same color <br>
 are adjacent, with the colors in the order red, white and blue. <br>
Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.<br>
Note:<br>
You are not suppose to use the library's sort function for this problem.<br>
click to show follow up.<br>
Follow up:<br>
A rather straight forward solution is a two-pass algorithm using counting sort.<br><
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of<br>0's, then 1's and followed by 2's.<br>
Could you come up with an one-pass algorithm using only constant space?<br>