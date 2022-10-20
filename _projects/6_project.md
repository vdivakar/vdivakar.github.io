---
layout: page
title: Deep De-mosaicing
description: De-mosaicing using CNNs
img: assets/img/demosaic.jpg.webp
importance: 4
category: past #work
---

Demosaicing using CNNs (Samsung)
A camera sensor captures single channel image where each pixel contains only 1 color information. The process of interpolating the remaining 2 colors via neighboring pixels to construct a full colored image is called Demosaicing. We used a deep learning model to approach this problem.
Key learning:
 - Used a ResNet-Bottleneck based deep learning architecture.
 - Wrote the architecture from scratch in Tensorflow 1.x to conduct multiple experiments
 - Residual learning; skip connections
 - Links - [Paper](https://link.springer.com/chapter/10.1007/978-981-15-4018-9_16) | [Pre-print](https://easychair.org/publications/preprint/NFnj)