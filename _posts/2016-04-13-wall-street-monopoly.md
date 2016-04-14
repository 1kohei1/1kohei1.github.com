---
layout: post
title: "Wall Street Monopoly"
description: ""
category: 
tags: [Algorithm]
---
{% include JB/setup %}
I was working on [Wall Street Monopoly](https://lpc.ucfprogrammingteam.org/localFiles/local2012PracticeProblems.pdf) at UCF Local Programming Contest in 2012. My professor explained this is [Matrix Chain Multiplication](https://en.wikipedia.org/wiki/Matrix_chain_multiplication), but it took me a while to get how to apply Matrix Chain Multiplication to this problem. So here is a little note for myself.

Wiki's pseudocode doesn't save the generated matrix dimension from multiplication, and I didn't get how `p[]` computes the cost of multiplication, so I created 3D array to save the result of multiplication of matrix.

Here is my basic code for Matrix Chain Multiplication

{% highlight java %}
// Get input data
// n is how many matrixes we have
// matrix is a global variable that stores row and col of each matrix
matrix = new int[n][2];
for (int i = 0; i < n; i++) {
	matrix[i] = new int[]{scanner.nextInt(), scanner.nextInt()};
}

// matrixDimension is a global variable that stores the dimension of multiplied matrix from i through j
matrixDimension = new int[n][n][2];
for (int i = 0; i < n; i++) {
	for (int j = i; j < n; j++) {
		if (i == j) {
			// if i == j, store its dimension
			matrixDimension[i][j] = matrix[i];
		} else {
			// If it is multiplied matrix, stores the row of the first matrix and column of the second matrix
			matrixDimension[i][j] = new int[]{matrixDimension[i][j - 1][0], matrix[j][1]};
		}
	}
}
{% endhighlight %}

Then, to calculate the minimum multiplication cost, I do it recursively and save the result of calculation in 2D array `memo`

{% highlight java %}
// This is in main function
System.out.println(solve(0, n - 1));

// The basic idea for this function is well explained in the section of [A Dynamic Programming Algorithm](https://en.wikipedia.org/wiki/Matrix_chain_multiplication#A_Dynamic_Programming_Algorithm)
public static int solve(int start, int end) {
	// If start and end is the same, return 0 since no multiplication occurs
	if (start == end) {
		return 0;
	}
	
	// If we already calculated this once, return saved value
	if (memo[start][end] != -1) {
		return memo[start][end];
	}
	
	int answer = Integer.MAX_VALUE;
	for (int i = start; i < end; i++) {
		// Partition matrix from i to k and k to j.
		// This reminds me merge sort
		int a = solve(start, i) + solve(i + 1, end) + matrixDimension[start][i][0] * matrixDimension[start][i][1] * matrixDimension[i + 1][end][1];
		answer = Math.min(answer, a);
	}
	memo[start][end] = answer;
	return answer;
}
{% endhighlight %}

So here is my core code for Matrix Chain Multiplication. I changed this code to this. The change I made is how I set up `matrixDimension` and the value I add in `solve` function.

{% highlight java %}
// Read data is the same

// This function has changed
public static void setDimension() {
	for (int i = 0; i < n; i++) {
		for (int j = i; j < n; j++) {
			if (i == j) {
				dimension[i][j] = blocks[i];
			} else {
				// I changed here.
				// For x, I add x of both matrix
				int x = dimension[i][j - 1][0] + blocks[j][0];
				// For y, I keep the bigger value
				int y = Math.max(dimension[i][j - 1][1], blocks[j][1]);
				// And use them to set multiplied or fused matrix dimension
				dimension[i][j] = new int[]{x, y};
			}
		}
	}
}

// 
public static long solve(int start, int end) {
	if (start == end) {
		return 0;
	}
	if (memo[start][end] != -1) {
		return memo[start][end];
	}
	
	long answer = Long.MAX_VALUE;
	for (int i = start; i < end; i++) {
		// The value I add here has been changed to follow the problem.
		long a = solve(start, i) + solve(i + 1, end) + 100 * Math.min(dimension[start][i][0], dimension[start][i][1]) * Math.min(dimension[i + 1][end][0], dimension[i + 1][end][1]);
		answer = Math.min(answer, a);
	}
	memo[start][end] = answer;
	return answer;
}
{% endhighlight %}

Here is all my change I made! Summarixing this as a document helps me to grasp what I did. Hope this helps future programmers!