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
- extractive summariztion, where salient sentences/segments of text are identified as important segments and directly copied into the summary (similr to highlighting text with a marker). 
- abstractive summarizatio, where the the generated saummary is a paraphrased of the important part of the text and hence more similar to human generaed summaries 

Prior to the hype of deep learning, TextRank and LexRank were two popular methods for extractive sumariztion. TextRank was mainly used for single document
and LexRank was mainly used for multi document summariztion. Both TextRank and LexRank create a graph of sentences and run the page rank algotihm 
to get the most important sentences (basically centroids in the graph). The edges between sentences are based on semantic similarity and content overlap. 
LexRank uses cosine similarity of TF-IDF vectors of sentences and TextRank uses the number of words two sentences have in common  normalized by sentences length.

LexRank uses the score of sentences from the page rank algorithm as a feature in a larger system with other features such as sentence’s position, sentence length. 
[source](https://en.wikipedia.org/wiki/Automatic_summarization)


# Evaluation:
When training a model for summarization, one can use cross-entropy (similar to language modeling task) to train the model. The offline evaluation metrics arenpoorly correzlted with human judgement and ignores important features such as factual correctnes. 
For offline evaluation one can use:
- ROUGE metric, [ROUGE: A Package for Automatic Evaluation of Summaries](https://www.aclweb.org/anthology/W04-1013.pdf)
ROUGE is the standard automatic evaluation measure for evaluating summarization tasks. 
```math
SE = \frac{\sigma}{\sqrt{n}}
```

{% raw %}
  $$a^2 + b^2 = c^2$$ --> note that all equations between these tags will not need escaping! 
 {% endraw %}
 
  - diadvantages:
  - not suitable for abtractive summariztion since it is based on n-gram overlaps
  - biased toward shorter summarizes
- ROUGE-WE (R-WE): instead of hard lexical matching of bigrams, R-WE uses soft matching based on the cosine similarity of word embeddings.
- ROUGE 2.0  leverages synonym dictionaries, such as WordNet, and considers all synonyms of matched words when computing token overlap. [ROUGE 2.0: Updated and Improved Measures for Evaluation of Summarization Tasks](https://arxiv.org/abs/1803.01937).
- [Co-opNet: Cooperative Generator–Discriminator Networks for Abstractive Summarization with Narrative Flow](https://arxiv.org/abs/1907.01272)
- METEOR: [An Automatic Metric for MT Evaluation with Improved Correlation with Human Judgments](https://www.cs.cmu.edu/~alavie/METEOR/pdf/Banerjee-Lavie-2005-METEOR.pdf) 
- BERTScore: [BERTScore: Evaluating Text Generation with BERT](https://arxiv.org/abs/1904.09675)
 BERTSCORE computes a similarity score for each token in the candidate sentence with each token in the reference sentence. However, instead of exact matches, they compute token similarity using contextual embeddings.  BERTSCORE computes the similarity of two sentences as a sum of cosine similarities between their tokens’ embeddings.
  - Advantages: BERTSCORE addresses two common pitfalls in n-gram-based metrics such as  BLEU, ROUGE, and METEOR. 
(1) First, such methods often fail to robustly match paraphrases.  This leads to performance underestimation when semantically-correct phrases are penalized because they differ from the surface form of the reference.
Second, n-gram models fail to capture distant dependencies and penalize semantically-critical ordering changes. For example, given a small window of size two, BLEU will only mildly penalize swapping of cause and effect clauses (e.g. A because B instead of B because A), especially when the arguments A and B are long phrases.


Similarity (embedding reference summary, embedding generated summary)
Human: grammar, punctuation, interesting, information quality, duplication, diversity, brevity




When training we can use a combination of supervised learning and RL to directly optimize for brevity, duplication, diversity, etc




