---
id: 93f47e4f-849b-45cc-b250-e3d674c20b7f
title: Keypoint-detection-and-description
desc: ''
updated: 1606202988543
created: 1606196809674
---
# Keypoint Detection and Description Simultaneously

- tags: [[detection-and-describe]]

还是和之前一样先说。不出意外，现在几乎都是detector和descriptor一起去学了，这个任务进展非常大。个人觉得比较有意思的几个工作：首先是CVPR'19的[[paper.D2-Net]](<https://github.com/mihaidusmanu/d2-net)，这篇大意是说detector其实没必要特意去学，直接从descriptor里取depth-wise> maximum和local spatial maximum就可以得到。如果沿着这个方向做，甚至detector都没必要特意设计loss去学（这个loss真的挺难设计的），确实是个很吸引人的性质。但现在d2-net的keypoint localization还是很不准，这对geometry computation影响还是很大，所以如果用来做sfm或者slam这种对geometry很敏感的任务估计还不太行。最近还有一篇[[paper.R2D2]] (<https://arxiv.org/abs/1906.06195>) 会比d2-net复杂一些，不过看实验结果似乎localization error小了很多，如果以后开源可以多测下。不过D2-Net和R2D2都依赖dense gt correspondences, 比如D2-Net依赖MegaDepth，而R2D2是用EpicFlow自己插值出来的，获取成本和精度都是麻烦事...所以最近有一篇[[paper.Unsuperpoint]]，完全[[paper.Self-supervised]]方法只用homography transformation（这点其实和[[paper.Superpoint]]很像，不过做成了self-improving，比[[paper.Superpoint]]优雅）去做，看起来效果也相当不错，期待它开源了再仔细测一测了。

