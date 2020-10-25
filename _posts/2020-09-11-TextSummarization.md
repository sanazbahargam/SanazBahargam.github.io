---
title: 'Text Summarization'
date: 2020-04-28
permalink: /posts/2020/09/TextSummarization/
tags:
  - NLP
  - Text Summarization
  - Text
---

Automatic summarization is the process of shortening a set of data computationally, to create a subset (a summary) that represents the most important or 
relevant information within the original content. Text summarization finds the most informative sentences in a document. 

Therea are two general approches to text summarziation:
- extractive summariztion
- abstractive summarizatio

Prior to the hype of deep learning, TextRank and LexRank were two popular methods for extractive sumariztion. TextRank was mainly used for single document
and LexRank was mainly used for multi document summariztion. Both TextRank and LexRank create a graph of sentences and run the page rank algotihm 
to get the most important sentences (basically centroids in the graph). The edges between sentences are based on semantic similarity and content overlap. 
LexRank uses cosine similarity of TF-IDF vectors of sentences and TextRank uses the number of words two sentences have in common  normalized by sentences length.

LexRank uses the score of sentences from the page rank algorithm as a feature in a larger system with other features such as sentence’s position, sentence length. 
[source](https://en.wikipedia.org/wiki/Automatic_summarization)


# Evaluation:
When training a model for summarization, one can use cross-entropy (similar to language modeling task) to train the model. 
For offline evaluation one can use:
- ROUGE metrics 
-- diadvantages:
  -- not suitable of abtractive summariztion since it is based on n-gram overlaps)
  -- biased toward shorter summarizes
- ROUGE-WE (R-WE): instead of hard lexical matching of bigrams, R-WE uses soft matching based on the cosine similarity of word embeddings.
- BERTScore: [BERTScore: Evaluating Text Generation with BERT](https://arxiv.org/abs/1904.09675)
 BERTSCORE computes a similarity score for each token in the candidate sentence with each token in the reference sentence. However, instead of exact matches, they compute token similarity using contextual embeddings.  BERTSCORE computes the similarity of two sentences as a sum of cosine similarities between their tokens’ embeddings.
Advantages: BERTSCORE addresses two common pitfalls in n-gram-based metrics such as  BLEU, ROUGE, and METEOR. 
(1) First, such methods often fail to robustly match paraphrases.  This leads to performance underestimation when semantically-correct phrases are penalized because they differ from the surface form of the reference.
Second, n-gram models fail to capture distant dependencies and penalize semantically-critical ordering changes. For example, given a small window of size two, BLEU will only mildly penalize swapping of cause and effect clauses (e.g. A because B instead of B because A), especially when the arguments A and B are long phrases.


Similarity (embedding reference summary, embedding generated summary)
Human: grammar, punctuation, interesting, information quality, duplication, diversity, brevity




When training we can use a combination of supervised learning and RL to directly optimize for brevity, duplication, diversity, etc




