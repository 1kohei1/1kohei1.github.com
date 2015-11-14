---
layout: post
title: "Sorting Algorithms"
description: "Insertion Sort, Bubble Sort, Selection Sort, Merge Sort, and Quick Sort"
category: 
tags: [Algorithm]
---
{% include JB/setup %}

I learned about sorting algorithm, so this is my implementation in C.

[Bubble Sort](https://en.wikipedia.org/wiki/Bubble_sort) O(n^2)

Very straightforward algorithm to sort numbers in array: compare one and next one. If the first one is bigger and next one, swap them. Repeat this iteration twice to make sure the value at index 0 can travel index n - 1. 

{% highlight C %}
void bubbleSort(int* num, int n) {
    int i, j;
    for (i = n - 1; i > 0; i--) {
        for (j = 0; j < n - 1; j++) {
            if (num[j] > num[j + 1]) {
                int temp = num[j + 1];
                num[j + 1] = num[j];
                num[j] = temp;
            }
        }
    }
    printArray(num, n);
}
{% endhighlight %}

[Insertion Sort](https://en.wikipedia.org/wiki/Insertion_sort) O(n^2)

Anytime when you find smaller element than previous element, go back and find the element that is smaller than the element the program is looking at. If it is already sorted, runtime analysis for Insertion Wort is O(n).
{% highlight c %}
void insertionSort(int* num, int n) {
    int i, j;
    for (i = 1; i < n; i++) {
        for (j = i; j > 0; j--) {
            if (num[j - 1] > num[j]) {
                int temp = num[j];
                num[j] = num[j - 1];
                num[j - 1] = temp;
            }
        }
    }
    printArray(num, n);
}
{%endhighlight %}

[Selection Sort](https://en.wikipedia.org/wiki/Selection_sort) O(n^2)

Start from the tail of the array, find the biggest one, and swap the tail and biggest element. Next, don't include the last element of array and find the biggest one. Swap the biggest one with the tail. Repeat this till you only have one element.
{% highlight C %}
void selectionSort(int* num, int n) {
    int i, j;
    for (i = n - 1; i >= 0; i--) {
        int maxIndex = 0;
        for (j = 0; j <= i; j++) {
            if (num[maxIndex] <= num[j]) {
                maxIndex = j;
            }
        }
        int temp = num[i];
        num[i] = num[maxIndex];
        num[maxIndex] = temp;
    }
    printArray(num, n);
}
{% endhighlight %}

[Merge Sort](https://en.wikipedia.org/wiki/Merge_sort) O(nlog n)

Split an array into two arrays. Sort each array and merge two sorted array into the original one. My code is not clearn, but it helped me understand how merge sort works. Keep this recursively.
{% highlight C %}
void mergeSort(int* num, int low, int high) {
    if (high - low + 1 == 2) {
        if (num[low] > num[high]) {
            int temp = num[high];
            num[high] = num[low];
            num[low] = temp;
        }
    } else if (high - low + 1 < 2) {
    } else {
        int mid = (low + high) / 2;
        mergeSort(num, low, mid);
        mergeSort(num, mid + 1, high);
        merge(num, low, mid + 1, high);
    }
}

void merge(int* num, int low, int mid, int high) {
    int lowIndex = low;
    int highIndex = mid;
    int index = low;
    int i;
    int mergedNum[high - low + 1];

    while (lowIndex <= mid || highIndex <= high) {
        int val = -1;
        if (lowIndex > mid) {
            val = num[highIndex];
            highIndex++;
        } else if (highIndex > high) {
            val = num[lowIndex];
            lowIndex++;
        } else {
            if (num[lowIndex] < num[highIndex]) {
                val = num[lowIndex];
                lowIndex++;
            } else {
                val = num[highIndex];
                highIndex++;
            }
        }
        mergedNum[index - low] = val;
        index++;
    }
    for(i = 0; i <= high - low; i++) {
        num[i + low] = mergedNum[i];
    }
}
{% endhighlight %}

[Quick Sort](https://en.wikipedia.org/wiki/Selection_sort) O(n^2)

Pick a random element that is used as pivot. Start at the beginning of array and end of the array. Increment starting index while the element is less than or equal to pivot number. Decrement the end of the array index while the element is greater than or equal to pivot. If low is less than high, swap low index element and high index element. If low is greater than high, swap high and pivot number. Split array into before high and after high. Repeat the same thing recursively.
{% highlight C %}
// start and end is the range of array that is being sorted.
// start and end is inclusive
void quickSort(int* array, int start, int end) {
    // Take care of error cases
    if (start >= end) {
        return;
    } else if (end - start == 1) {
        if (array[end] < array[start]) {
            swap(array, start, end);
        }
        return;
    }
    int randomIndex = generateRandomBetween(start, end);
    int pivotNum = array[randomIndex];

    // Variables for moving in array
    int low = start;
    int high = end;

    swap(array, low, randomIndex);
    low++;
    while(low < high) {
        // Increment low
        while(low <= high && array[low] <= pivotNum) {
            low++;
        }
        // Decrement high
        while(low <= high && pivotNum <= array[high]) {
            high--;
        }
        if (low < high) {
            swap(array, low, high);
        }
    }
    // Swap pivot and high
    swap(array, start, high);
    quickSort(array, start, high - 1);
    quickSort(array, high + 1, end);
}

// Generate random value
// start and end is inclusive
int generateRandomBetween(int start, int end) {
    return rand() % (start - end + 1) + start;
}

// Swap element in array at index1 and index2
void swap(int* array, int index1, int index2) {
    int temp = array[index1];
    array[index1] = array[index2];
    array[index2] = temp;
}

{% endhighlight %}

I like quicksort the best since I spent a lot of time to understand what is going on. Hope my code helps you to implement them!