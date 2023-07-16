+++
title = "GPT vs BERT"
description = "Notes on GPT and BERT"
date = "2023-05-27"
aliases = ["gpt vs bert"]
author = "Benjamin Hong"
math = true
+++

### » GPT: Generative Pre-trained Transformer
GPT consists of stacked transfomer decoder layers. Text input is fed into a text and position embedding layer, which yields an embedding that is fed into the stacked decoder layers. At the end of these layers, output probabilities of the form $P(w_i|w_{i-k},\ldots,w_{i-1})$ are produced. The model is pre-trained using a language modeling objective that maximizes
$$L_1=\sum_i \log P(w_i|w_{i-k},\ldots,w_{i-1};\Theta)$$

GPT is fine-tuned on specific supervised problems. For classification tasks, training examples consist of input tokens and output labels in the form $((x_1,\ldots,x_m),y)$. The pre-trained model can be applied to the input sequence $(x_1,\ldots,x_m)$ and then a linear model can be trained using the last transformer layer to predict $y$. For this classification task, the objective would be to maximize
$$L_2 = \sum_{((x_1,\ldots,x_m),y)}\log P(y|x_1,\ldots,x_m)$$

During the fine-tuning process, the pre-trained transformer weights should continue to be trained on the new task. This gives us the following objective functions.
$$L_1 = \sum_{(x_1,\ldots,x_m)}\sum_{i=1}^m\log P(x_i|x_{i-k},\ldots,x_{i-1})$$
$$L_2 = \sum_{((x_1,\ldots,x_m),y)}\log P(y|x_1,\ldots,x_m)$$

Our overall objective would be to maximize
$$L=\lambda L_1 + L_2$$

### » BERT: Bidirectional Encoder Representations from Transformers
BERT consists of stacked transformer encoder layers. This means that representations can contain the entire input sequence, rather than only the left context. It uses a masked language model objective for pre-training and next sentence prediction as its secondary objective. It takes in two sentences packed together in the input which are separated by a [SEP] symbol. The first position of the input is a [CLS] token that is used for computing a single representation of the input for classification tasks. The last layer of the BERT architecture outputs a representation for each input token.

To achieve the masked language model objective, a softmax layer is used to predict the token in each position. Some of the input tokens in each sequence, typically 15%, are replaced with a [MASK] symbol. The goal is to minimize the cross-entropy loss on the output predictions of the masked tokens.

The next sentence prediction objective, which is trained jointly with the masked language model objective, is used to obtain representations that capture dependencies between sentences. The [CLS] token is used in this task, where the model must make binary predictions such as deciding if sentence 2 comes after sentence 1.

BERT fine-tuning is task-specific. For sequence tasks, the output representations can be used to make predictions for each token. For classification tasks, [CLS] representations can be used to make predictions.