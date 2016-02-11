---
layout: post
title: "Bitwise Operator"
description: "Learned about bitwise operator. So note about bitwise operator"
category: 
tags: []
---
{% include JB/setup %}
I learned bitwise operator, so here is the note for my learning. This [link](https://www.hackerearth.com/notes/bit-manipulation/) helped me a lot to understand what and how useful they are.
Here are some functions I created to master bitwise opereator. Most of them are from the link above.

{% highlight java %}
public static boolean isPowerOf2(int n) {
	return n != 0 && ((n & (n - 1)) == 0);
}

public static int powerOf2(int power) {
	return 1 << power;
}

public static int count1InBinary(int n) {
	int count = 0;
	while (n != 0) {
		n = n & (n - 1);
		count++;
	}
	return count;
}

// i starts from 0
public static boolean isIth1InBinary(int n, int i) {
	if ((n & (1 << i)) != 0) {
		return true;
	} else {
		return false;
	}
}

// Recursively O(n^3)
public static void printSubsets(char[] elements, int index, int[] a) {
	if (index == elements.length) {
		for (int i = 0; i < a.length; i++) {
			if (a[i] == 1) {
				System.out.printf("%c", elements[i]);
			}
		}
		System.out.println();
	} else {
		printSubsets(elements, index + 1, a);
		a[index] = 1;
		printSubsets(elements, index + 1, a);
		a[index] = 0;
	}
}

// Bitwisely O(n^3)
public static void printAllSubsets(char[] elements) {
	int n = elements.length;
	for (int i = 0; i < 1 << n; i++) {
		for (int j = 0; j < n; j++) {
			if ((i & (1 << j)) != 0) {
				System.out.printf("%c", elements[j]);
			}
		}
		System.out.println();
	}
}
{% endhighlight %}

I found a [link](http://www.graphics.stanford.edu/~seander/bithacks.html) that lists many functions that take advantages of bitwise operator.