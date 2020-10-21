---
title: 'Transformers 2'
date: 2020-09-22
permalink: /posts/2020/09/Transformers2/
tags:
  - NLP
  - Transformers
  - MARGE
  - ConveRT
  - Generalization through Memorization
  - AdapterHub
  - T5
---
This blog post is the continuation of my previous blog post, [Transformers](https://sanazbahargam.github.io/posts/2020/07/Transformers/). In my previous blog post, I explained original Transformer paper, BERT, GPT, XLNet, RoBERTa, ALBERT, BART, and AMBER. 
In this blog post, I will explain MARGE, ConveRT, Generalization through Memorization, AdapterHub, and T5.



# Pre-training via Paraphrasing - MARGE (Multilingual Autoencoder that Retrieves and Generates
[Paper](https://arxiv.org/abs/2006.15020) from Facebook AI

[Presenation in ACL 2020, “Beyond BERT”](https://slideslive.com/38929793/beyond-bert) by Mike Lewis
![pic](https://github.com/sanazbahargam/SanazBahargam.github.io/blob/master/images/MARGE.png?raw=true)


In this paper, authors tried grounding natural language into the reality of our world instead of MLM. The problem with next token predictions MLM is that they focus only on linguistic form, they learn the characteristics of coherent language without necessarily associating meaning to it. 

MARGE is a pre-trained sequence-to-sequence model learned with an unsupervised multilingual multi-document paraphrasing objective.
During pre-training, the input to the model is a batch of evidence documents z1..M and target documents x1..N . The model is trained to maximize the likelihood of the targets, conditioned on the evidence documents, and the relevance of each evidence document to each target: 
- The model first computes a relevance score f(xi , zj ) between every pair of documents xi and zi , by embedding each document and computing their cosine similarities. 
- The model then computes the likelihood of reconstructing each xi conditioned on z1..M and each f(xi , ·), using a modified seq2seq model. The similarity score encourages the model to attend more to relevant evidence documents. Backpropagating the reconstruction loss therefore improves both the sequence-to-sequence model and the relevance model. 
- They construct batches so that evidence documents are relevant to the targets, using the relevance model for retrieval

A truly remarkable outcome is that MARGE can perform decent zero-shot machine translation that is, without any fine-tuning on parallel data

# ConveRT: Efficient and Accurate Conversational Representations from Transformers
[Paper](https://arxiv.org/abs/1911.03688) by PolyAI

![pic](https://github.com/sanazbahargam/SanazBahargam.github.io/blob/master/images/ConveRT.png?raw=true)

They used shared parameters, quantization and less number of layers, but instead used a very long sequence input (for conversation it’s needed) and reduced the number of parameters by order of magnitude. 


# Generalization through Memorization: Nearest Neighbor Language Models
[Paper](https://arxiv.org/abs/1911.00172)  from Facebook AI and Stanford   

[Presenation in ACL 2020, “Beyond BERT”](https://slideslive.com/38929793/beyond-bert) by Mike Lewis

![pic](https://github.com/sanazbahargam/SanazBahargam.github.io/blob/master/images/GeneralizationMemorization.png?raw=true)

The main contribution: Improvement for downstream tasks which need factuality like QA
The paper introduces kNN-LM, an approach that extends a pre-trained LM by linearly interpolating its next
word distribution with a k-nearest neighbors (kNN) model. The nearest neighbors are computed
according to distance in the pre-trained embedding space and can be drawn from any text collection, including the original LM training data. This approach allows rare patterns to be memorized
explicitly, rather than implicitly in model parameters. It also improves performance when the same
training data is used for learning the prefix representations and the kNN model, strongly suggesting
that the prediction problem is more challenging than previously appreciated.


# Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer, T5
[Paper](https://arxiv.org/abs/1910.10683) from Google
![pic](https://1.bp.blogspot.com/-o4oiOExxq1s/Xk26XPC3haI/AAAAAAAAFU8/NBlvOWB84L0PTYy9TzZBaLf6fwPGJTR0QCLcBGAsYHQ/s1600/image3.gif?raw=true)


# AdapterHub: A Framework for Adapting Transformers
[Paper](https://arxiv.org/pdf/2007.07779v1.pdf) from Technical University Darmstadt, New York University, CIFAR, University of Cambridge,DeepMind

![pic](https://github.com/sanazbahargam/SanazBahargam.github.io/blob/master/images/ConveRT.png?raw=true)

AdapterHub enables you to perform transfer learning of generalized pre-trained transformers such as BERT, RoBERTa, and XLM-R to downstream tasks such as question-answering, classification, etc. using adapters instead of fine-tuning. Adapters serve the same purpose as fine-tuning but do it by stitching in layers to the main pre-trained model, and updating the weights Φ of these new layers, whilst freezing the weights θ of the pre-trained model. As you might imagine, this makes adapters much more efficient, both in terms of time and storage, compared to fine-tuning. Adapters have also been shown to be able to match the performance of state-of-the-art fine-tuning methods!


