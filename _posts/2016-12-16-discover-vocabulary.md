---
layout: post
title:  "Discovering Semantic Vocabularies"
date:   2016-12-16 16:55:00
categories: text-mining
tags: feature text-mining topics code-example
---

Word embeddings are dense vectors used to represent word meanings. Both [Stanford's GloVe](https://nlp.stanford.edu/projects/glove/) and [Google's word2vec](https://www.tensorflow.org/tutorials/word2vec) are open source packages and provide efficient implementations to train these vectors. Many pretrained vectors can be found online. I download [the pretrained word vectors](http://nlp.stanford.edu/data/glove.6B.zip) from the GloVe web. The vectors look like below, in each line a word is represented as a multidimentional vector of float values:

```python
pretrained = open("glove.6B/glove.6B.50d.txt", "r").readlines()
for line in pretrained[:3]:
	print line
```

<pre class="console"><code>the 0.418 0.24968 ... -0.18411 -0.11514 -0.78581
, 0.013441 0.23682 ... -0.56657 0.044691 0.30392
. 0.15164 0.30177 ... -0.35652 0.016413 0.10216</code></pre>

I'm going to perform a clustering analysis on these vectors. First I prepare the vocabulary table to easily look up words and the embedding matrix for clustering:

```python
import numpy
id2word = []
id2vec = []
for line in pretrained[:10000]:
	data = line.split(" ")
	id2word.append(data[0])
	id2vec.append(numpy.array([float(d) for d in data[1:]]))
```

The [scikit-learn package](http://scikit-learn.org/stable/modules/clustering.html) in Python provides a rich library of clustering algorithms. K-means is one of the most commonly used algorithms. You can customize the number of clusters to form with `n_clusters`, here i choose 100.

```python
from sklearn.cluster import KMeans 
kmeans = KMeans(n_clusters=100).fit(numpy.array(id2vec))
```

So the vocabularies in each cluster are:

```python
word_cluster = []
for c in range(100):
	word_cluster.append([])

for i, c in enumerate(kmeans.labels_):
	word_cluster[c].append(id2word[i])

for words in word_cluster[:5]:
	print words
```

<pre class="console"><code>['williams', 'mike', 'tom', 'bob', 'steve', ...]
['i', 'we', 'you', 'what', 'him', ...]
['visit', 'summer', 'events', 'trip', 'festival', ...]
['$', 'million', 'total', '100', 'estimated', ...]
['support', 'process', 'organization', 'effort', 'launched', ...]</code></pre>

It's fun to discover semantically similar words using the method and adjusting the parameters. But it's better if you first obtain a set of vectors which can perfectly represent word meanings!