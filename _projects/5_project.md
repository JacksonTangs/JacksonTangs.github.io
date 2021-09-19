---
layout: post
title: 火灾监测模型
description: 基于 WSN 的环境火灾监测模型的安全性研究及实现
---

This project is my work from from March to August in 2019 , work with Liyao Tong, [Zijian Zhao](https://www.researchgate.net/profile/Zijian-Zhao-11), Qian Su and Defan Xue, supervised by by [Prof. Yingxu Lai](http://dmslab.hkg03.bdysite.com/index.php/people/yingxu-lai/) and [LECT. Jing Liu](https://english.bjut.edu.cn/info/1152/1586.htm). We invent a fire monitoring system that is resistant to collusion attacks. And posted the work as a [patent](https://cprs.patentstar.com.cn/Search/Detail?ANE=8BFA9EGB9GDC5AFA9EHD9EHD9GIFCHHAAIDA9IEH8CGAAHHA) .

In the process of rapid economic development, the issue of natural resource protection is particularly important. The protection of vegetation resources against fire is an important aspect. The frequent occurrence of large-scale forest and grassland fires in recent years, where the source of fire is not controlled in time, is a major problem, indicating the lack of a highly timely and effective fire monitoring system in this area.

Combining the advantages of flexible distribution, large scale and dynamic monitoring of Wireless Sensor Networks (WSN), this work proposes a grassland fire monitoring model with hierarchical detection of WSN nodes and secure data transmission. In terms of node security detection within the WSN, the node security is detected layer by layer from the sensor nodes collecting data, to the cluster head aggregating data, and then to the gateway. In WSN nodes based on time correlation, differential filtering is applied to obtain sensor anomaly time series; based on spatial correlation, improved D-S evidence theory model and proximity detection model are applied to distinguish malicious and faulty nodes, discard malicious node data, reduce the impact of malicious injection data on the model and improve the model detection accuracy; finally, based on event correlation, malicious nodes are verified by temperature field The WSN performs data analysis in real time, resisting joint attacks by complicit nodes and enabling low-cost, more efficient monitoring of fire occurrences and maximising the reduction of losses caused by fires. In terms of secure data transmission within the WSN, the routing is done through an ant colony algorithm that improves the way pheromone concentration is calculated to select the data transmission path. This method reduces WSN energy consumption, avoids local power depletion of the system, and considers link quality and path trust to reduce transmission packet loss rate, greatly reducing the overall security risk, preventing information leakage in transmission and improving the efficiency of message transmission. In addition, to ensure secure data sharing after data transmission, proxy re-encryption based on shamir threshold is applied to ensure the confidentiality, integrity and authenticity of data in the wireless sensor network by using symmetric encryption mechanism for sensor data.

The collection environment of the meadow dataset used in the WSN node security detection part of this work is the Huahai grassland in Dulan County, Qinghai Province, and the industrial lathe sensor production collection dataset provided by the Aliyun Tianchi competition is used in the data security transmission part. After experimental comparison, it is proved that the correlation-based node detection model can locate the scope of fire occurrence more accurately and resist the wrong data injection attack by the complicit nodes to achieve normal monitoring under the attack. Secure data transmission enables optimal path finding, greatly reducing link consumption, and proxy re-encryption mechanisms ensure secure data sharing.

<img src="./fig1.png"  div align=center />

<img src="./fig2.png"  div align=center />

<img src="./fig3.png"  div align=center />

<img src="./fig4.png"  div align=center />

<img src="./fig5.png"  div align=center />

