# cnn-feature-hierarchy

[Rich feature hierarchies for accurate object detection and semantic segmentation](https://arxiv.org/pdf/1311.2524.pdf)

## Introduction

> Our approach combines two key insights:
> (1) one can apply high-capacity convolutional neural networks (CNNs) to bottom-up region proposals in order to
> localize and segment objects and (2) when labeled training
> data is scarce, supervised pre-training for an auxiliary task,
> followed by domain-specific fine-tuning, yields a significant
> performance boost. Since we combine region proposals
> with CNNs, we call our method R-CNN: Regions with CNN
> features

Findings:
- On the 200-class ILSVRC2013 detection dataset, R-CNN’s
mAP is 31.4%

## Model

- Region Proposal: 
  - [Selective search for object recognition](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf)
  - [Regionlets for Generic Object Detection](https://openaccess.thecvf.com/content_iccv_2013/papers/Wang_Regionlets_for_Generic_2013_ICCV_paper.pdf)

- Feature extraction.

> We extract a 4096-dimensional feature vector from each region proposal using the Caffe [24]
implementation of the CNN described by Krizhevsky et
al. [25]. Features are computed by forward propagating
a mean-subtracted 227 × 227 RGB image through five convolutional layers and two fully connected layers. We refer
readers to [24, 25] for more network architecture details

## Datasets

These are useful huggingface datasets for later reference:

- `nateraw/pascal-voc-2012`
- `imagenet-1k`
- `zh-plus/tiny-imagenet`

## Motivation

I am interested in this paper due to wanting to actually reproduce the results
of other papers that reference this paper including:

- [Deep Visual-Semantic Alignments for Generating Image Descriptions](https://arxiv.org/pdf/1412.2306.pdf)

    - Pre-trained on Imagenet
    - Fine tuned using 200 classes
    - 64x64 images

    Top 19 detected locations + full image:
    > v = Wm[CNNθc(Ib)] + bm

    - CNN(Ib) is fully connected layer before classifier
    - θc parameters 60 million
    - Wm is h x 4096.
    - h is multimodal embedding size (1k to 1.6k) and is the ultimate 
    - Image ultimately represented as set of h-dim vectors
        - vi = {v1, v2, ... 20}
    - v1..19 are top 19 detected locations
    - v20 is whole image

- [Deep fragment embeddings for bidirectional image sentence mapping](https://arxiv.org/pdf/1406.5679.pdf)

## TODO

- [ ] Get familiar with how to train and eval on images
  - [ ] Train a classifier on a small set of images
    - [X] Pick the dataset - cifar10
    - [ ] Setup train and eval harness
    - [ ] Understand performance
  - [ ] Consider object detection instead of classification
- [ ] Look at `Selective Search for Object Recognition` and understand the dataset needed and how to evaluate quality of region proposals