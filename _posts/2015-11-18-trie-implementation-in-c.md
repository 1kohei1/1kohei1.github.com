---
layout: post
title: "Trie Implementation in C"
description: "Trie Implementation in C"
category: 
tags: [Algorithm]
---
{% include JB/setup %}
Hello, I learned Trie in my CS1 class, and implemented it. So, let me share my code!
My struct for trie looks like this
{% highlight c %}
struct trie {
	int isWord;
	struct trie* nextLetter[26];
};
{% endhighlight %}

And, my code for creating single node, and inserting a word looks like this.
{% highlight c %}
struct trie* createSingleTrie() {
	struct trie* temp = malloc(sizeof(struct trie));
	temp->isWord = 0;

	int i;
	for (i = 0; i < 26; i++) {
		temp->nextLetter[i] = NULL;
	}
	return temp;
}

void insertWord(struct trie* dictionary, char word[], int index, int wordLength) {
	if (index == wordLength) {
		dictionary->isWord = 1;
		return;
	}
	if (dictionary->nextLetter[word[index] - 'a'] == NULL) {
		dictionary->nextLetter[word[index] - 'a'] = createSingleTrie();
	}
	insertWord(dictionary->nextLetter[word[index] - 'a'], word, index + 1, wordLength);
}

int isInDictionary(struct trie* dictionary, char word[], int index, int length) {
	if (dictionary == NULL) {
		return 0;
	}
	if (index == length) {
		return dictionary->isWord;
	}
	return isInDictionary(dictionary->nextLetter[word[index] - 'a'], word, index + 1, length);
}
{% endhighlight %}
It is a bit long to put all codes here, so check out my [Github Gist](https://gist.github.com/1kohei1/a77bd3d26250d9776a80)!