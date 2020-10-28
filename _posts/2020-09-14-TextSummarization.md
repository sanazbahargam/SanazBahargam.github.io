---
title: 'Text Summarization'
date: 2020-09-14
permalink: /posts/2020/09/TextSummarization/
tags:
  - NLP
  - Text Summarization
  - ROUGE
  - BERTSCORE
  - METEOR 
  - DSR
---

Automatic summarization is the process of shortening a set of data computationally, to create a subset (a summary) that represents the most important or relevant information within the original content. Text summarization finds the most informative sentences in a document. 

# Strategies for generating summaries 
Therea are two general approches to text summarziation:
- extractive summarization, where salient spans of text are identified as important segments and directly copied into the summary (similar to highlighting text with a marker). 
- abstractive summarization, where the generated summary is a paraphrased of the important part of the text and hence more similar to human-generated summaries 
- Hybrid models, combines extractive and abstractive summarization and include two phases, content selection, and paraphrasing.

Prior to the hype of deep learning, TextRank and LexRank were two popular methods for extractive summarization. TextRank was mainly used for a single document
and LexRank was mainly used for multi-document summarization. Both TextRank and LexRank create a graph of sentences and run the page rank algorithm to get the most important sentences (basically centroids in the graph). The edges between sentences are based on semantic similarity and content overlap. 
LexRank uses cosine similarity of TF-IDF vectors of sentences and TextRank uses the number of words two sentences have in common normalized by sentence length.

LexRank uses the score of sentences from the page rank algorithm as a feature in a larger system with other features such as sentence position, sentence length. 
[source](https://en.wikipedia.org/wiki/Automatic_summarization)


# Evaluation:
When training a model for summarization, one can use cross-entropy (similar to language modeling task) to train the model. The offline evaluation metrics are poorly correlated with human judgment and ignores important features such as factual correctness. 
The offline evaluation metrics can be categorized into the following groups.
## n-GRAM Matching Metrics
### ROUGE metric
[ROUGE: A Package for Automatic Evaluation of Summaries](https://www.aclweb.org/anthology/W04-1013.pdf)
ROUGE is the standard automatic evaluation measure for evaluating summarization tasks. 

![pic](https://github.com/sanazbahargam/SanazBahargam.github.io/blob/master/images/ROUGEMetric.png?raw=true)
 
- disadvantages:
- not suitable for abstractive summarization since it is based on n-gram overlaps. It expects the generated summary to be identical to the reference summary and does not recognize synonym concepts. It also doesn't capture subset coverage (it focuses on the complete set of n-gram overlap).
- biased toward shorter summarizes
### ROUGE-WE (R-WE)
[Better Summarization Evaluation with Word Embeddings for ROUGE](https://www.aclweb.org/anthology/D15-1222.pdf)
instead of hard lexical matching of bigrams, R-WE uses soft matching based on the cosine similarity of word embeddings.
### ROUGE-G
[A Graph-theoretic Summary Evaluation for ROUGE](https://www.aclweb.org/anthology/D18-1085.pdf)
 combines lexical and semantic matching by applying graph analysis algorithms to the
WordNet semantic network
### ROUGE 2.0  
leverages synonym dictionaries, such as WordNet, and considers all synonyms of matched words when computing token overlap. [ROUGE 2.0: Updated and Improved Measures for Evaluation of Summarization Tasks](https://arxiv.org/abs/1803.01937). To address ROUGE's problems, the authors propose the following metrics:
 ### ROUGE-{N|Topic|TopicUniq}+Synonyms 
 It captures synonyms using a synonym
dictionary (synonym dictionary customizable by application and domain)
- ROUGE-Topic - topic or subset coverage (topic customizable by POS occurrence)
- ROUGE-TopicUniq- unique topic or subset coverage (topic customizable by POS
occurrence)
### METEOR 
[An Automatic Metric for MT Evaluation with Improved Correlation with Human Judgments](https://www.cs.cmu.edu/~alavie/METEOR/pdf/Banerjee-Lavie-2005-METEOR.pdf) 
based on a generalized concept of unigram matching between the machine produced translation and human-produced
reference translations. Unigrams can be matched based on their surface forms, stemmed forms, and meanings; furthermore, METEOR can be easily extended to
include more advanced matching strategies. Once all generalized unigram matches between the two strings have
been found, METEOR computes a score for this matching using a combination of unigram-precision, unigram-recall, and a measure of fragmentation that is designed
to directly capture how well-ordered the matched words in the machine translation are in relation to the reference.

## Embedding Based Metrics
### Distributional Semantics Reward (DSR) 
[Deep Reinforcement Learning with Distributional Semantic Rewards for Abstractive Summarization](https://arxiv.org/abs/1909.00141)
Given that contextualized word representations (such as ELMO, BERT, GPT) have shown that they have a powerful capacity of reflecting distributional semantic, the authors propose to use the distributional semantic reward to boost the reinforcement learning-based abstractive summarization system.
- Advantages: 
    - DSR does not rely on cross-entropy loss (XENT) to produce readable phrases. Thus, no exposure bias is introduced.
    - DSR improves generated tokens’ diversity and fluency while avoiding unnecessary repetitions.

<!--###  [Co-opNet: Cooperative Generator–Discriminator Networks for Abstractive Summarization with Narrative Flow](https://arxiv.org/abs/1907.01272) -->

### BERTScore
[BERTScore: Evaluating Text Generation with BERT](https://arxiv.org/abs/1904.09675)
 BERTSCORE computes a similarity score for each token in the candidate sentence with each token in the reference sentence. However, instead of exact matches, they compute token similarity using contextual embeddings. In another word,  BERTSCORE focuses on sentence-level generation evaluation
by using pre-trained BERT contextualized embeddings to compute the similarity between two sentences as a weighted aggregation of cosine similarities between their tokens. BERTScore  has a higher correlation with human evaluation on text generation
tasks comparing to the existing evaluation metric
![pic](https://github.com/sanazbahargam/SanazBahargam.github.io/blob/master/images/BERTScore.png?raw=true)
 
- Advantages: BERTSCORE addresses two common pitfalls in n-gram-based metrics such as  BLEU, ROUGE, and METEOR. 
    - First, such methods often fail to robustly match paraphrases.  This leads to performance underestimation when semantically-correct phrases are penalized because they differ from the surface form of the reference.
    - Second, n-gram models fail to capture distant dependencies and penalize semantically-critical ordering changes. For example, given a small window of size two, BLEU will only mildly penalize swapping of cause and effect clauses (e.g. A because B instead of B because A), especially when the arguments A and B are long phrases.
  
## Human Judgement, Learned Metrics
 - relevance (selection of important content from the source)
 - consistency (factual alignment between the summary and the source) 
 - fluency (quality of individual sentences)
 - coherence (collective quality of all sentences)
 - Grammer
 - Information Quality
 - Duplication
 - Fiversity
 - Brevity



<!-- When training we can use a combination of supervised learning and RL to directly optimize for brevity, duplication, diversity, etc-->


