---
layout: post
title: "Dijkstra's Algorithm Implementation in Java"
description: "Dijkstra's Algorithm Implementation in Java"
category: 
tags: [Algorithm]
---
{% include JB/setup %}

This post is about [Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm).
I was working on [Dijkstra: Shortest Reach 2](https://www.hackerrank.com/challenges/dijkstrashortreach/submissions/code/15417507) on hackerrank and have to learn Dijkstra's algorithm to pass their time limit. Floyd-Warshall was my first approach, but it couldn't solve some test data under their time.

So this is how I implemented. 

{% highlight java %}
public static void dijkstra(int start, int end) {
	ArrayList<Integer> queue = new ArrayList<Integer>();
	queue.add(start);
	dist[start] = 0;
	
	while(queue.size() != 0) {
		int curr = queue.remove(0);
		
		for (int i = 0; i < map.length; i++) {
			if (map[curr][i] != 0 && visited[i] == 0 && dist[curr] + map[curr][i] < dist[i]) {
				dist[i] = dist[curr] + map[curr][i];
			}
		}
		int nextNode = nextNode();
		if (nextNode == -1 || nextNode == end) {
			return;
		}
		visited[curr] = 1;
		queue.add(nextNode);
	}
}
{% endhighlight %}

The run time analysis of this function is O(n^2). The worst case is to put all nodes into queue, and n times to get the minimum value. The Wikipedia page about Dijkstra's algorithm says the algorithm runs in O(E + V * logV). E is the number of edges, and V is the number of nodes. This is done by using min-priority queue implemented by [Fibonacci heap](https://en.wikipedia.org/wiki/Fibonacci_heap). 

Since I was not familiar with Fibonacci heap, I implemented by myself. But will update the function once figure out how to implement fibonacci heap later on. This [video](https://www.youtube.com/watch?v=gdmfOwyQlcI) helped me to learn how things work. My entire test cases and input/output codes are found on [Github gist](https://gist.github.com/1kohei1/b2ab4c1cd44d9596c86e).