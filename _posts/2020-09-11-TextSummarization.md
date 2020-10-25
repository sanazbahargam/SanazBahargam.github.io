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
(source)[https://en.wikipedia.org/wiki/Automatic_summarization]  





