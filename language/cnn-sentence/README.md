# cnn-sentence

[Convolutional Neural Networks for Sentence Classification](https://arxiv.org/pdf/1408.5882.pdf)

## Introduction

> Convolutional neural networks (CNN) utilize layers with convolving filters that are applied to local features (LeCun et al., 1998). Originally invented for computer vision, CNN models have subsequently been shown to be effective for NLP and have achieved excellent results in semantic parsing (Yih et al., 2014), search query retrieval (Shen et al., 2014), sentence modeling (Kalchbrenner et al., 2014), and other traditional NLP tasks (Collobert et al., 2011).

See https://chriskhanhtran.github.io/posts/cnn-sentence-classification/ for a deep dive into solving this which was also used as a reference.

## Model

The model is a Simple CNN: One layer of convolution on top of word vectors. The word vectors come from [word2vec](https://code.google.com/archive/p/word2vec/)


- `Xi` is `k`-dimensional word vector for `i`-th word
- Sentence length n
- `X1-n = x1 | x2 | ... | xn`  combined with concatenation operation
- filter `w` involves `h` words
- Feature `ci = f(w )`
- f is nonlinearity ( e.g. tanh )
- output is feature map

The model is a variation on `Natural Language Processing (Almost) from Scratch` https://www.jmlr.org/papers/volume12/collobert11a/collobert11a.pdf

## Hyper Parameters & Tuning

- Use RLU
- Filter windows `h` of 3, 4, 5 w /100 feature maps
- dropout rate `p` of 0.5
- l2 constraint (s) of 3
- mini-batch size of `50`
- Training is done through stochastic gradient descent over shuffled mini-batches with the Adadelta update rule (Zeiler, 2012).

NOTE: I don't know what `Adadelta update rule` is yet.

## Datasets

Movie Review Polarity dataset: https://www.cs.cornell.edu/people/pabo/movie-review-data/review_polarity.tar.gz