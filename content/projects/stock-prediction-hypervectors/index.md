+++
title = "Forecasting stock movement using principal component analysis and hyperdimensional computing"
description = "Stock movement prediction project"
date = "2023-11-27"
aliases = ["stock prediction hypervectors"]
author = "Benjamin Hong"
math = true
+++

### » Introduction
Forecasting stock price movement is a problem that investors and researchers have long been tackling. This is a challenging task due to the wide variety of factors that impact stock prices, which span from exchange rates to monetary policy to current events. Being able to accurately predict the movement of prices would generate large amounts of profit, making this research area of high interest for investors and researchers alike. Many traditional methods of time series forecasting that are popular in finance, such as logistic regression and ARIMA, are based on the assumption that values come from a linear process. However, this is a vast oversimplification, resulting in inaccurate predictions for nonlinear stock price movements. For this reason, newer approaches like deep learning methods have been gaining popularity recently due to their ability to capture nonlinear processes.

In particular, neural network architectures such as CNNs, RNNs, and LSTMs have shown promising results. Yang et al. [1] details a state-of-the-art model which combines a CNN and an LSTM to predict the direction of price movements. By using the CNN for feature extraction and LSTM for prediction, this hybrid model is able outperform other models such as ANN, SVM, and CNN. However, this level of performance is achieved through using a large number of neurons that scales upwards as the number of features increases. As a result, these models are computationally expensive and require large amounts of memory. The complexity of these models also result in high training times, since each iteration of the training process requires applying all of the training data to the model and updating parameters using gradient descent. Furthermore, the complexity of these models results in a lack of transparency that makes it difficult to decipher how decisions are made.

In this paper, a methodology for stock movement prediction using principal component analysis and hyperdimensional computing is proposed as an alternative to neural network-based methods. HDC is based around performing operations on high-dimensional vectors called hypervectors, which can represent multiple pieces of information within a single entity. If successful, this methodology will be able to achieve similar levels of success as state-of-the-art models with lower training times and higher transparency. Furthermore, HDC is more robust to hardware faults due to the large size of hypervectors, whereas traditional ANNs can be significantly impacted if errors such as bit flips cause changes in data representation. This study aims to create a design that combines the advantages of PCA in feature extraction with the advantages of HDC in classification.

### » Proposed Framework

To implement this, the architecture will consist of four major components: data representation, feature extraction, hypervector encoding, and prediction.

#### A. Data Representation

The historical data of the S&P 500 index will be used for this study. Class labels will indicate the direction of stock movement, which will be determined by looking at the daily close prices of the index. Given close price $C_t$ for the $t$-th day, the assigned class label will be $1$ if $C_{t+1} > C_t$ and $0$ otherwise.

According to Patel et al. [2], using deterministic trend signals improves feature extraction and consequently model performance, so a variety of technical indicators will be converted into deterministic trend signals. See the table below for exact details on how these indicators and signals are to be computed. These are the same indicators and signals used in [1].

![Table of indicators and signals](images/indicator-signal-table.png)

#### B. Feature Extraction
Since the focus of this paper will be on prediction using HDC and less so on the methods used for feature extraction, PCA will be used due to its simplicity in implementing.

#### C. Hypervector Encoding
The vectors obtained from PCA will be encoded into hypervectors. This will be done by using the baseline HDC implementation described in Basaklar et al. [3], which follows the steps below.

First, the minimum and maximum values of each feature $f_n$ (where $1 \leq n \leq N$ and $N$ is the number of features) will be used to create quantization functions $q_n$ that return a quantization level from $1$ to $M$ when given a value for the feature.

Next, level $1$ of each feature will be assigned a random hypervector $L_n^1 \in \{−1, 1\}^D$, where $D$ is the hypervector dimension. The remaining level hypervectors from $L_n^2$ to $L_n^M$ will be generated by randomly flipping $\frac{D}{2M-1}$ bits.

Using the level hypervectors and the post-PCA vectors, sample hypervectors $H_s$ will be created for each sample $x_s$ (where $1 \leq s \leq S$ and $S$ is the number of samples). To do this, the quantization levels for each feature in $x_s$ will be found using $q_n$. Then, the corresponding level hypervectors $L_n^{q_n(x_s)}$ will added together:

$$H_s = \sum_{n=1}^N L_n^{q_n(x_s)} \qquad \forall s \in \{1,2,\ldots,S\}$$

Finally, the class hypervectors can be constructed by summing together all of the hypervectors of the same class. Given a class $k$, its representative hypervector $\mathcal{C}_k$ will be calculated as

$$\sum_{s=1}^S H_s I_k(H_s)$$

where $I_k$ is the indicator function (i.e. $I_k(H_s)$ equals $1$ when $y_s=k$ and $0$ otherwise).

#### D. Prediction
The predicted class label of a query hypervector $q$ corresponds with the class hypervector that yields the highest cosine similarity:

$$y_{\text{pred}} = \text{argmax} \frac{q \cdot \mathcal{C}_k}{\|q\|\|\mathcal{C}_k\|}$$

### To be updated!