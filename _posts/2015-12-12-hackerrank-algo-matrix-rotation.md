---
layout: post
title: "Hackerrank: [Algo] Matrix Rotation"
description: "My solution/code to hackerrank [Algo] Matrix Rotation problem"
category: 
tags: [Hackerrank]
---
{% include JB/setup %}
- Hackerrank problem link: [[Algo] Matrix Rotation problem](https://www.hackerrank.com/challenges/matrix-rotation-algo)
- My rotation approach: [Github gist](https://gist.github.com/1kohei1/396b2d7450bab54558e3)
- My final approach: [Github girst](https://gist.github.com/1kohei1/278395e592f9c820a693)

First I wrote rotate function that rotates one digit in anti-clockwise direction for the entire function. Then, call that function `numRotation` times. However, this was very expensive. So I decided to get all digits in the circle, counts how many elements in that circle, and calculates how many times the number has to be shifted. 

With this approach, everything runs under time constraints. 

My rotate function:
{% highlight java %}
public static int[][] rotate(int[][] map, int row, int col) {
	int[][] newMap = new int[row][col];
	int rowStart = 0;
	int colStart = 0;
	
	while (rowStart * 2 < row && colStart * 2 < col) {
		// Top
		for (int i = colStart  +1; i < col - colStart; i++) {
			newMap[rowStart][i - 1] = map[rowStart][i];
		}
		// Right
		for (int i = rowStart + 1; i < row - rowStart; i++) {
			newMap[i - 1][col - colStart - 1] = map[i][col - colStart - 1];
		}
		// Bottom
		for (int i = colStart; i < col - colStart - 1; i++) {
			newMap[row- rowStart - 1][i + 1] = map[row - rowStart - 1][i];
		}
		// Left
		for (int i = rowStart; i < row - rowStart - 1; i++) {
			newMap[i + 1][colStart] = map[i][colStart];
		}
		rowStart++;
		colStart++;
	}

	return newMap;
}
{% endhighlight %}

My entire code is in the main function, so please refer to my [Github girst](https://gist.github.com/1kohei1/278395e592f9c820a693) located at the top for my final code. The reason why I did this in the main function is I was not sure how I should update my `map` variable in the function. 

Anyway, this problem was easy to figure out, but hard to implement. Good problem hackerrank!!