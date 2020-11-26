---
id: 5bc96717-b624-46ed-afff-6c08666793a2
title: D2-net
desc: ''
updated: 1606362472269
created: 1606196867098
---
# D2-Net

## Paper Data

- 2019, CVPR
- title: D2-Net: A Trainable CNN for Joint Description and Detection of Local Features
- tags: [[pkm.Keypoint]], [[detection-and-describe]]

## [[detection-and-describe]] Paradigm

- Classical interest point detection and description method where separated handcrafted methods are used to first identify repeatable keypoints and then represent them with a local descriptor.
- Illustration
  - ![https://remnote-user-data.s3.amazonaws.com/9fLcaaEHF93T7XMf6h9zTACHMAqDIGaPhZ4_giEAAXE9_ddPlTjg--DrL21MB6i9jvK3bJ9hP0nJ06MwOsoINiQMsnhGzy16uUtaLDVJFHfYYNE5xp-6C9oqOYbnMwdH](https://remnote-user-data.s3.amazonaws.com/9fLcaaEHF93T7XMf6h9zTACHMAqDIGaPhZ4_giEAAXE9_ddPlTjg--DrL21MB6i9jvK3bJ9hP0nJ06MwOsoINiQMsnhGzy16uUtaLDVJFHfYYNE5xp-6C9oqOYbnMwdH) 

## 1. Feature Description

$$
f(x) = sin(x)
$$

- Interpretatioin of feature 3D tensor $F$ is a dense set $\mathbf{d}$ :
$$
\mathbf{d}_{ij} = F_{ij}, \mathbf{d}\in{\mathbb{R}^n}
$$

- where $n$ is channel size, $i=1,\cdots, h$, $j=1,\cdots,w$.
- Compare using [[pkm.L2-norm]]

## 2. Feature Detection

- Collection of 2D responses $D$ from 3D tensor $F$ :
$$ 
D^k=F\_{: :k}, D^k\in{\mathbb{R}^{h\times w}}
$$
  - where $n$ is channel size, $k==1,\cdots,n$.

- ### Hard Feature Detection
  - For a point $(i,j)$ to be detected, we need:
  (3)   $(i,j)$ is a detection $\Longleftrightarrow D_{ij}^k$ is a local max in $D^k$
      with $k=\argmax\limits_t D_{ij}^t$.

- ### Soft Feature Detection
  1. Amenable for back propagation.
  2. Define a soft local-max score
  - (4)      $\alpha_{ij}^k=\exp(D_{ij}^k)/\sum_{(i^{\prime},j^{\prime})\in\mathcal{N}(i,j)} \exp(D_{i'j'}^k)$ where $\mathcal{N}(i,j)$ is the set of 9 neighbours of pixel $(i,j)$.
  3. Define a soft channel selection to compute a [[pkm.Ratio-to-max]] per descriptor that emulates channel-wise non-maximum suppression:
  - (5)     $\beta_{ij}^k = D_{ij}^k/\max\limits_t D_{ij}^t$  
  4. Together we maximize the product of both scores across all feature maps $k$ to obtain single score map:
  - (6)     $\gamma_{ij}=\max\limits_k (\alpha_{ij}^k \beta\_{ij}^k$)
  5. Image-level normalization:
  - (7)     $s_{ij}=\gamma_{ij} / \sum\limits_{(i',j')} \gamma_{i'j'}$

- ### Multi-scale Detection
  - TODO
  - Need more time to read!

