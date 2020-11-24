---
id: 93f47e4f-849b-45cc-b250-e3d674c20b7f
title: '-keypoint-detection-and-description'
desc: ''
updated: 1606197242888
created: 1606196809674
---

# Keypoint Detection and Description Simultaneously

- tags: [[detection-and-describe]]

现在几乎都是detector和descriptor一起去学了，这个任务进展非常大。个人觉得比较有意思的几个工作：首先是CVPR'19的[[D2-Net]](https://github.com/mihaidusmanu/d2-net)，这篇大意是说detector其实没必要特意去学，直接从descriptor里取depth-wise maximum和local spatial maximum就可以得到。如果沿着这个方向做，甚至detector都没必要特意设计loss去学（这个loss真的挺难设计的），确实是个很吸引人的性质。但现在[[D2-Net]]的keypoint localization还是很不准，这对geometry computation影响还是很大，所以如果用来做sfm或者slam这种对geometry很敏感的任务估计还不太行。最近还有一篇[[R2D2]] (https://arxiv.org/abs/1906.06195) 会比[[D2-Net]]复杂一些，不过看实验结果似乎localization error小了很多，如果以后开源可以多测下。不过D2-Net和R2D2都依赖dense GT correspondences, 比如[[D2-Net]]依赖MegaDepth，而[[R2D2]]是用[[EpicFlow]]自己插值出来的，获取成本和精度都是麻烦事...所以最近有一篇[[Unsuperpoint]]，完全[[Self-supervised]]方法只用homography transformation（这点其实和[[Superpoint]]很像，不过做成了self-improving，比[[Superpoint]]优雅）去做，看起来效果也相当不错，期待它开源了再仔细测一测了。