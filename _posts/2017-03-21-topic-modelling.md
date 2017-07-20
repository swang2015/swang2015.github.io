---
layout: post
title:  "Probabilistic Topic Modelling"
date:   2017-03-21 10:35:00
categories: text-mining
background: /images/bg/bg_sakura.jpg
tags: feature text-mining topics code-example
math: true
---

Topic modelling is a technique to automatically discover the hidden topics in each document. The basic idea is that words with similar meaning will occur in similar documents. A document is then modeled and described by topics coverages with word distributions. _Latent Semantic Indexing (LSI)_ and _Latent Dirichlet Allocation (LDA)_ are two common models. Practically the models perform similarly.

<div class="post-img">
	<img src="/images/nlp/topic.jpg" width="60%">
</div>

Knowing a set of documents _d<sub>1</sub>, ..., d<sub>m</sub>_ and vocabulary words _w<sub>1</sub>, ..., w<sub>n</sub>_, we can construct a document-term matrix @@X \in \mathbb{R}^{m \times n}@@ where @@x_{ij}@@ describes the occurrence of word _w<sub>j</sub>_ in document _d<sub>i</sub>_ and can be count, 0-1, or tf-idf. 

We decompose **_X_** with @@X = U_t \Sigma V_t^T@@ with truncated SVD and get @@U_t@@ and @@V_t@@ representing topic weights in each document and word weights in each topics repectively. This method is the _LSI_.

_Probabilistic LSI (pLSI)_ deals with probabilities instead. The Model is @@P(w\|d) = P(d)\sum_t P(t\|d)P(w\|t)@@ and can be trained with EM algorithm. However, the model lacks knowledge to compute for new documents and the number of parameters grows as amount of documents increase.

_LDA_ improves _pLSI_ by imposing Dirichlet priors _α_ and _β_ to document-topic and topic-word distribution. LDA posits that the topics covered from both observed and unseen documents is drawn from a distribution _Dirichlet(α)_ and words in a topic is drawn from another distribution _Dirichlet(β)_. Now we only need to worry about _α_ and _β_.

<div class="post-img">
	<img src="/images/nlp/graph-lda.png" width="35%">
</div>
<p class="post-cap">Graphical model representation of LDA</p>

The pyscript that I used to implement topic models is [here](https://github.com/swang2015/data-science-messy-snippets/blob/master/text-mining/topic-modelling.py). I started with tokenizing and stemming each documents:

```python
def preprocess(text):
	stop = set(stopwords.words('english'))
	stemmer = SnowballStemmer("english")

	doc_tokenized = word_tokenize(text.decode('utf-8').lower())
	doc_stop_stem = [word for word in doc_tokenized if re.search('[a-zA-Z]', word) and (word not in stop)]
	return doc_stop_stem
```

The corpus is transformed in to either _bag of words_ or _tfidf_ vectors.
```python
class topic_model():
	def prepare_doc(self, fname):
		...
		self.dictionary = corpora.Dictionary(self.docs)
		self.corpus = [self.dictionary.doc2bow(doc) for doc in self.docs]
		self.tfidf = models.TfidfModel(self.corpus, id2word=self.dictionary)
		self.corpus_tfidf = self.tfidf[self.corpus]
```

The process can be implemented with lda, lsi or log entropy model.

```python
class topic_model():
	def train(self, method='lda_tfidf', K=10):
		if method == 'lda_tfidf':
			logging.info("Training LDA model with tfidf.")
			self.model = models.LdaModel(corpus=self.corpus_tfidf, num_topics=K, id2word=self.dictionary)
		elif method == 'lda':
			logging.info("Training LDA model.")
			self.model = models.LdaModel(corpus=self.corpus, num_topics=K, id2word=self.dictionary)
		elif method == 'lsi_tfidf':
			logging.info("Training LSI model with tfidf.")
			self.model = models.LsiModel(corpus=self.corpus_tfidf, num_topics=K, id2word=self.dictionary)
		elif method == 'logentropy':
			logging.info("Training log-entropy model.")
			self.model = models.LogEntropyModel(corpus=self.corpus, id2word=self.dictionary)
		else:
			msg = "Unknown semantic method %s." % method
			logging.error(msg)
			raise NotImplementedError(msg)
```

The topic models are especially useful for calculating document similarities, finding related documents to a new query, and discovering semantic words.

