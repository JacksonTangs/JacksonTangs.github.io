---
layout: post
title: A project for protocol reverse engineering
description: Relational reasoning-based approach for network protocol reverse engineering 
---
This project is my diploma thesis from Dec. 2020 to Aug. 2021, supervised by [Prof. Yipeng Wang](https://sites.google.com/site/yipengwang1/home) and [Prof. Yingxu Lai](http://dmslab.hkg03.bdysite.com/index.php/people/yingxu-lai/). 

<img src="./RelaNet-architecture.png"  div align=center />

Most format inference methods need sequence alignment to deal with variable-length fields. However, it alignment quality doesn't perform well. In this study, we address the problem of how to mitigate the impact from variable-length fields in inferring protocol format specifications. We propose a novel relational reasoning-based approach to learn the **context relations** between keywords. This type of relation can be used to diminish the impacts of variable-length fields, which would normally strongly impair the quality of protocol format inference.

To the best of our knowledge, our method is the first to address protocol format inference with deep learning.

The paper is being reviewed, thus detailed information will be added later.
