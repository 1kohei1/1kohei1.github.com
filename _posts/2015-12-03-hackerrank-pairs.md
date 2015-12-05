---
layout: post
title: "Hackerrank: Pairs"
description: "Explain different approach to hackerrank problem Pairs"
category: 
tags: [Algorithm]
---
{% include JB/setup %}

- Hackerrank problem link: [link](https://www.hackerrank.com/challenges/pairs)
- Two pointer approach: [Github gist](https://gist.github.com/1kohei1/f393dab3ed3d12f17748)
- Binary search approach: [Github girst](https://gist.github.com/1kohei1/bb68f6357e7cd74306d0)

I solved this problem by two pointer approach at first. However, when I read the editorial, it mentioned using binary search tree. I found that is really clever, and decided to try that binary search tree to compare how fast it can run.

My code is on Github gist. Look them up if you are interested in how I wrote them. If you are interested in performance difference, keep reading.

This is the result with two pointer implementation:
![two pointer result]({{ site.url }}/assets/two-pointer-result.png)

And here is the binary search implementation result:
![binary search result]({{ site.url }}/assets/binary-search-tree-result.png)

Look at how fast binary search tree runs! This is amazing!! It runs by 0s for some test cases.

It is awesome that if you pick a right solution, your program solve the problem in incredible speed!