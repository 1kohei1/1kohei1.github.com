---
layout: post
title: "Binary Heap Structure"
description: "Wrote binary heap structure in C"
category: 
tags: [Data Structure]
---
{% include JB/setup %}

I was studying for the CS1 final and wrote a program to understand binary heap more. So I want to share it. I didn't fully test it, and if you enter more than 2 digit numbers, the visualization of heap messes up. So play with only 2 digit numbers. Also, I am using -1000 to indicate that spot is not filled yet, so it doesn't work right if you enter -1000. Alternative for this is making another 1D array to save if that index is filled in or not. Anyway, you can start from my code and change whatever you want!

I will put some code here, and entire code on [Github gist](https://gist.github.com/1kohei1/ee0dd0f73112312e0e19).
{% highlight c %}
int* initialize_min_heap() {
    int* min_heap = malloc(sizeof(int) * MIN_HEAP_SIZE);
    int i;
    for (i = 1; i < MIN_HEAP_SIZE; i++) {
        min_heap[i] = DEFAULT_VALUE;
    }
    return min_heap;
}

void insert(int* min_heap, int num) {
    int index = 1;
    // Insert
    while (index < MIN_HEAP_SIZE) {
        if (min_heap[index] == DEFAULT_VALUE) {
            min_heap[index] = num;
            break;
        }
        index++;
    }
    // Check if children is greater than parents elements
    while (index / 2 != 0) {
        int parentNum = min_heap[index / 2];
        if (parentNum > min_heap[index]) {
            min_heap[index / 2] = min_heap[index];
            min_heap[index] = parentNum;
        }
        index /= 2;
    }
}
{% endhighlight %}
Enjoy!!