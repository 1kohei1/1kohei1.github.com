---
layout: post
title: "Bolts and Nuts (no duplicates)"
description: ""
category: 
tags: [Algorithm]
---
{% include JB/setup %}
Hi everyone! I learned bolts and nuts algorithm in the class, so let me share my code.
The problem is basically this

	You are given a collection of nuts of different size and corresponding bolts. You can choose any nut & any bolt together, from which you can determine whether the nut is larger than bolt, smaller than bolt or matches the bolt exactly. However there is no way to compare two nuts together or two bolts together. Suggest an algorithm to match each bolt to its matching nut.

I'm gonna put the quicksort code here, and entire code on [Github gist](https://gist.github.com/1kohei1/16a00108e9cc539087b0).
{% highlight java %}
// start: inclusive, end: inclusive
public static void matchRec(int[] a, int[] b, int start, int end) {
	if (start >= end) {
		return;
	}
	
	int aPivot = generateRandomIndex(start, end);
	int matchedBIndex = -1;
	
	int low = start;
	int high = end;
	
	while (low < high) {
		while (low <= end && b[low] <= a[aPivot]) {
			if (a[aPivot] == b[low]) {
				matchedBIndex = low;
			}
			low++;
		}
		
		while (start <= high && a[aPivot] <= b[high]) {
			if (a[aPivot] == b[high]) {
				matchedBIndex = high;
			}
			high--;
		}
		
		if (high < low) {
			break;
		}
		swap(b, low, high);
	}
	if (low < matchedBIndex) {
		swap(b, low, matchedBIndex);
		matchedBIndex = low;
	} else if (matchedBIndex < high) {
		swap(b, matchedBIndex, high);
		matchedBIndex = high;
	}
	
	low = start;
	high = end;
	
	while (low < high) {
		while (low <= end && a[low] <= b[matchedBIndex]) {
			low++;
		}
		
		while (start <= high && b[matchedBIndex] <= a[high]) {
			high--;
		}
		
		if (high < low) {
			break;
		}
		swap(a, low, high);
	}
	if (low < aPivot) {
		swap(a, low, aPivot);
		aPivot = low;
	} else if (aPivot < high) {
		swap(a, high, aPivot);
		aPivot = high;
	}
	
	matchRec(a, b, start, aPivot - 1);
	matchRec(a, b, aPivot + 1, end);		
}
{% endhighlight %}