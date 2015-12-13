---
layout: post
title: "Maximum subarray problem"
description: "Memo to get the maximum subarray problem. Also include the code to print out the range for that subarray"
category: 
tags: [Algorithm]
---
{% include JB/setup %}
- Problem Description on [Wiki](https://en.wikipedia.org/wiki/Maximum_subarray_problem)
- My code on [Github gist](https://gist.github.com/1kohei1/bef3d3056eef0ea1683a)

This is memo to get the max sum in the subarray of the array. If you just want to get the max value, this is the code
{% highlight java %}
int n = scanner.nextInt();
int max = 0;
int sumSoFar = 0;

for (int i = 0; i < n; i++) {
	sumSoFar += scanner.nextInt();
	if (sumSoFar < 0) {
		sumSoFar = 0;
	}
	if (max < sumSoFar) {
		max = sumSoFar;
	}
}
System.out.println(max);
{% endhighlight %}

`n` is the number of elements in the array. This code calculates the max value in the array. Then, I wondered what if I want the elements of the sub array? So I added the code to keep index of the subarray beginning and where the sub array ends.
{% highlight java %}
int n = scanner.nextInt();
int[] nums = new int[n];

int max = 0;
int sumSoFar = 0;
int startIndex = 0;
int endIndex = 0;

for (int i = 0; i < n; i++) {
	nums[i] = scanner.nextInt();
	
	if (sumSoFar == 0 && sumSoFar + nums[i] > 0) {
		startIndex = i;
	}
	
	sumSoFar += nums[i];
	if (sumSoFar < 0) {
		sumSoFar = 0;
	}
	if (max < sumSoFar) {
		max = sumSoFar;
		endIndex = i;
	}
}
System.out.println(max);
for (int i = startIndex; i <= endIndex; i++) {
	System.out.printf("%d ", nums[i]);
}
{% endhighlight %}
Now the code prints out the elements in the sub array!