---
title: 'Transformers'
date: 2020-07-30
permalink: /posts/2020/07/Transformers/
tags:
  - NLP
  - Transformers
  - BERT
  - AMBERT
  - ROBERTA
  - ALBERT
  
---

Transformers:
This post contains my notes throughout years on different transformers. These notes are very crude and not edited yet (more like my cheat sheets), but I thought to share it anyway. Please let me know if you have any comments or if you find any mistakes.


# Attention is all you need
![pic](https://github.com/sanazbahargam/SanazBahargam.github.io/blob/master/images/transformer_block.png =24x48)

Positional encoding
Using sin and cos functions, the earlier dimensions have smaller wavelengths and can capture short range offset, while the later dimensions can capture longer distance offset.

Transformer blocks are characterized by a multi-head self-attention mechanism, a position- wise feed-forward network, layer normalization modules and residual con- nectors. The input to the Transformer model is often a tensor of shape RB × RN , where B is the batch size, N the sequence length.

# GPT
![pic](https://github.com/sanazbahargam/SanazBahargam.github.io/blob/master/images/gpt.png)
ALL GPTs have only the transformer decoder (and not the encore part). In GPT first the model is pre-trained for LM tasks (causal LM) and then fine-tuned on the final task. They found that including language modeling as an auxiliary objective to the fine-tuning helped learning by (a) improving generalization of the supervised model, and (b) accelerating convergence. So the final objective is 
L3(C) = L2(C) + λ ∗ L1(C) 
in which L2 is the objective for labeled data and L1 is the objective for LM. 
Overall, larger datasets benefit from the auxiliary objective ( λ ∗ L1(C) ) but smaller datasets do not.

For Training, they used a modified version of L2 regularization with w=0.01 on all non-bias or gain weights. For the activation function, they used GELU. They also learned the position embeddings instead of the sinusoidal version. For fine-tuning, 3 epochs were sufficient for the most task and they set  λ =0.5

GPT1 was trained on book corpus (about 7K unpublished books), the context size (number of tokens)  os 512.

GPT2 was trained on outbound links from Reddit (the articles which were linked from Reddit) which received at least 3 karma (keeping only posts with a high number of upvotes)resulted to 45M links after filtering (removing Wikipedia pages etc) they ended up with 8M webpages, 40GB of text (around 10B tokens), model has 1.5B parameters (when 48 layers), size of vocab is 50.257K, context size is 1024 tokens (BERT was 512) and batch size 512. 
GPT2 data compression (tokens/parameters) = 10B/1.5B=6.66
SOTA in 7 out of 7 NLP benchmarks
Differences between GPT and GPT2:
Layer normalization was moved to the input of each sub-block, similar to a residual unit of type “building block” (differently from the original type “bottleneck”, it has batch normalization applied before weight layers).
An additional layer normalization was added after the final self-attention block.
A modified initialization was constructed as a function of the model depth.
The weights of residual layers were initially scaled by a factor of 1/√n where n is the number of residual layers.
Use larger vocabulary size and context size.


GPT3 has 175B parameters and is trained on 499B tokens (from common crawl, webtext2, books1, books2, Wikipedia). The 175 Billion parameters need 175*4=700GB memory (floating-point needs 4 bytes)
 
GPT3 data compression (tokens/parameters) = 499/175=2.85
GPT3 has lower data compression compared to GPT2 so, with this amount of parameters, whether the model functions by memorizing the data in the training and pattern matching in inference. 
 GPT-3 shows that it is possible to improve the performance of a model by "simply" increasing the model size, and in consequence, the dataset size and the computation (TFLOP) the model consumes. However, as the performance increases, the model size has to increase more rapidly. Precisely, the model size varies as some power of the improvement of model performance. Language model performance scales as a power-law of model size, dataset size, and the amount of computation.


# XLNet
Similar to Bert, Trained on booksCorpus and English Wikipedia (13GB of plain text) for pretraining. In addition, they include  Giga5(16 GB) ClueWeb (19G after filtering), Common Crawl (110 GB after filtering) for pretraining. In total, they have 32.89 B tokens.
XLNet-Large is similar to BERT-Large in model size and they use a sequence of 512. 
With a batch size of 8192, it took 5.5 days to train and still it under fits the data.
SOTA on 18 out of 20 NLP tasks.

XLNet combines the bidirectional capability of BERT with the autoregressive technology of Transformer-XL. One of the disadvantages of BERT is that BERT fails to model the joint probability of the predicted tokens, i.e. it assumes that predicted tokens ([MASK]s) are independent, AR models eliminate the independence assumption made in BERT.
XlNet has advantages of both AR (auro-regressive) and AE (auto-encoding) models. Since an AR language model is only trained to encode a unidirectional context (either forward or backward), it is not effective at modeling deep bidirectional contexts. On the contrary, downstream language understanding tasks often require bidirectional context information. This results in a gap between AR language modeling and effective pretraining. Firstly, instead of using a fixed forward or backward factorization order as in conventional AR models, XLNet maximizes the expected log likelihood of a sequence w.r.t. all possible permutations of the factorization order. Thanks to the permutation operation, the context for each position can consist of tokens from both left and right. In expectation, each position learns to utilize contextual information from all positions, i.e., capturing bidirectional context. 

