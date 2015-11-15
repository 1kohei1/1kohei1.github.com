---
layout: post
title: "Knapsack Problem"
description: "Study about knapsack problem"
category: 
tags: [Algorithm]
---
{% include JB/setup %}

Knapsack algorithm can be used to maximize combination of objects under restriction.
The sample knapsack problem looks like this.

	You have a knapsack and 4 objects. The knapsack can carry 20kg, and each object's weight is 3kg, 8kg, 9kg, and 8kg. Each object is worth $10, $4, $9, and $11 respectively. Which objects should you put into your knapsack to make the most valuable out of 4 objects?

The explanation about how to approach this problem is found [here](http://www.cs.ucf.edu/~dmarino/progcontests/modules/dp2/ProgTeamLecDP-2.pdf). Scroll down to page 6 starting with heading **Example #3: 0-1 Knapsack Problem**
My code for this problem is this. I basically copied and pasted from the link. I renamed variables and put comments for myself. 
{% highlight Java %}
public static void runKnapsach() {
	// The number of total objects we are using.
	int numObjects = 4;
	
	// Variables for storing weights and values
	int[] weights = new int[]{3, 8, 9, 8};
	int[] values = new int[]{10, 4, 9, 11};
	
	// Maximum weights that the knapsack can carry
	int maxWeights = 20;
	
	// Store the maximum value that the knapsack can carry if knapsack can carry index-kg at maximum
	int[] answers = new int[maxWeights + 1];
	
	// Set initial value 0, meaning its value is 0 for index-kg
	for (int i = 0; i <= maxWeights; i++) {
		answers[i] = 0;
	}
	
	for (int i = 0; i < numObjects; i++) {
		for (int j = maxWeights; j >= weights[i]; j--) {
			if (answers[j - weights[i]] + values[i] > answers[j]) {
				answers[j] = answers[j - weights[i]] + values[i];
			}
		}
	}
	
	System.out.println(answers[maxWeights]);
}
{% endhighlight %}

#### Runtime Analysis
The code I presented above takes `numObjects × maxWeights`, because it is two nested loop. However, this problem can be solved by bruteforce. Altough bruteforce takes 2^n, the problem can be solved. Depending on the value of numObjects and maxWeights, bruteforce somestimes solve more efficient than knapsack algorithm.

For example, if numObjects = 5, maxWeights = 100000, bruteforce is better. If numObjects = 30, maxWeights = 1000, knapsack algorithm is better. 

Bruteforce code:
{% highlight java %}
static int maxValue = 0;

public static void runBruteForce() {
	int numObjects = 4;
	int maxWeights = 20;

	int[] weights = new int[]{3, 8, 9, 8};
	int[] values = new int[]{10, 4, 9, 11};
	
	bruteForce(0, weights, values, 0, 0, numObjects, maxWeights);
	System.out.println(maxValue);
}

public static void bruteForce(int index, int[] weights, int[] values, int weight, int value, int numObjects, int maxWeights) {
	if (index == numObjects) {
		if (weight <= maxWeights && value > maxValue) {
			maxValue = value;
		}
		return;
	}
//		To make it efficient a little bit
//		if (weight + weights[index] <= maxWeights) {
//			bruteForce(index + 1, weights, values, weight + weights[index], value + values[index], numObjects, maxWeights);
//		}
	bruteForce(index + 1, weights, values, weight + weights[index], value + values[index], numObjects, maxWeights);
	bruteForce(index + 1, weights, values, weight, value, numObjects, maxWeights);
}
{% endhighlight %}