---
layout: post
title: "Longest Common Substring/Subsequence"
description: "Longest Common Substring/Subsequence algorithm"
category: 
tags: [Algorithm]
---
{% include JB/setup %}
I learned [Longest Common Substring](http://www.geeksforgeeks.org/longest-common-substring/) and [Longest Common Subsequence](http://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/), so here is my code.

{% highlight java %}
// Longest Common Subsequence
while(true) {
	char[] c1 = scanner.next().toCharArray();
	char[] c2 = scanner.next().toCharArray();
	
	int[][] map = new int[c1.length + 1][c2.length + 1];
	
	for (int i = 1; i < c1.length + 1; i++) {
		for (int j = 1; j < c2.length + 1; j++) {
			if (c1[i - 1] == c2[j - 1]) {
				map[i][j] = map[i - 1][j - 1] + 1;
			} else {
				map[i][j] = Math.max(map[i - 1][j], map[i][j - 1]);
			}
		}
	}
	
	// Print common sequence
	String commonS = "";
	int dx = c1.length;
	int dy = c2.length;
	
	while (dx > 0 && dy > 0) {
		if (c1[dx - 1] == c2[dy - 1]) {
			commonS = "" + c1[dx - 1] + commonS;
			dx--;
			dy--;
		} else {
			if (map[dx - 1][dy] > map[dx][dy - 1]) {
				dx--;
			} else if (map[dx - 1][dy] < map[dx][dy - 1]) {
				dy--;
			}
		}
	}
	System.out.printf("%d, %s\n", map[c1.length][c2.length], commonS);
}
{% endhighlight %}

{% highlight java %}
// Longest Common Substring
while(true) {
	char[] c1 = scanner.next().toCharArray();
	char[] c2 = scanner.next().toCharArray();
	
	int[][] map = new int[c1.length + 1][c2.length + 1];
	
	int answer = 0;
	int dx = 0;
	int dy = 0;
	
	for (int i = 1; i < c1.length + 1; i++) {
		for (int j = 1; j < c2.length + 1; j++) {
			if (c1[i - 1] == c2[j - 1]) {
				map[i][j] = map[i - 1][j - 1] + 1;
				if (answer < map[i][j]) {
					answer = map[i][j];
					dx = i;
					dy = j;
				}
			} else {
				map[i][j] = 0;
			}
		}
	}
	
	String commonS = "";
	while (true) {
		if (map[dx][dy] == 0) {
			break;
		}
		commonS = "" + c1[dx - 1] + commonS;
		dx--;
		dy--;
	}
	
	
	System.out.printf("%d: %s\n", answer, commonS);
}
{% endhighlight %}

I need to learn more algorithm.