---
layout: post
title: "HackerRank Palindrome Index Solution"
description: "My solution to hackerrank palindrome problem"
category: 
tags: [Hackerrank]
---
{% include JB/setup %}

I was working on Palindrome Index on [hackerrank.com](http://hackerank.com/). Then, I cannot solve [Palindrome Index](https://www.hackerrank.com/challenges/palindrome-index) problem.

My approach was

1. Run for loop from 0 to length - 1
2. Take ith character
3. Check if new string is palindrome.

This algorithm is very expensive since time complexity is O(n^2). But I didn't come up with any other solution. After reading [this](http://www.martinkysel.com/hackerrank-palindrome-index-solution/) blog post, I have much better understanding. 

Since the problem states the solution is guaranteed to exist, faster approach is like this.

1. Compare [0]th index and [last] index of the string
2. If they are different take the first character out, and check if that is palindrome
3. If it is palindrome, return the low index. If not, return high index.
4. Increment low and decrement high until s[low] differs from s[high] or low > high

Now, this runs much much faster than my first solution!! Wonderful!!

{% highlight java %}
public static int palindromeIndex(String a) {
	int low = 0;
	int high = a.length() - 1;
	
	while(low <= high) {
		if (a.charAt(low) != a.charAt(high)) {
			if (isPalindrome(a.substring(0, low) + a.substring(low + 1))) {
				return low;
			} else {
				return high;
			}
		}
		low++;
		high--;
	}
	return -1;
}
{% endhighlight %}