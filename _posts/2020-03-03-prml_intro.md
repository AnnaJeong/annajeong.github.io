--- 
title: "[PRML] Ch 1. Introduction"
excerpt: Introduction to Pattern Recognition and Machine Learning

categories:
    - PRML
tags:
    - Machine Learning
use_math: true
toc: true
toc_sticky: true
---
*This post is summary of the book Pattern Recognition and Machine Learning by Christopher M. Bishop*


## 1. Introduction


- pattern recognition is automatic discovery of regularities in data through computer algorithms
- we can perform tasks such as classification using these regularities found in the data
![figure1.1](../../assets/images/prml/figure1_1)
- Machine Learning can be used to find the digits of these handwritten digits
    - Though it could be tackled using handcrafted rules or heuristics, machine learning can give better results due to high variety of the data


### Machine Learning


- Machine Learning is the process of finding a functions $y(x)$ which takes new digit image $x$ and generates an output vector $y$, which has same format as the target vectors
- because the training data only contains a part of all possible input vector, **generalization** is central goal in pattern recognition
- pre-processing is done to make pattern recognition problem easier
    - it is sometimes called *feature extraction*
    - test data must be pre-processed using the same steps as the training data
    - pre-processing might be done to spped up computation
    - pre-processing must be done in a way it doesn't discard important information that might affect the overall accuracy


### Types of Machine Learning


- **Supervised Learning**: training data is comprised of input vectors and corresponding target vectors
    - Classification: target vectors are consisted of finite number of discrete categories
    - Regression: target vectors are consisted of one or more continuous variable
- **Unsupervised Learning**: training data comprised of input vectors without any corresponding target values
    - Clustering: disvocering groups of similar exampels within the data
    - Density reduction: determining the distribution of data within the input space
    - Visualization: projecting the data from a high-dimensional space down to two or three dimensions
- **Reinforement Learning**: the problem of finding suitable actions to take in given situation in order to maximize a reward
    - there is a sequence of states and actions which has to be discovered by trial and error
    - in many cases, the current action not only affects the immediate reward but also has an impact on the reward at all subsequent time steps

