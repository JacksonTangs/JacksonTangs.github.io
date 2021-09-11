---
layout: post
title: LBS security
description: Fake location generation algorithm based on LBS resistance to continuous query attacks
---

This project is my work in Jun. 2020 , work with [Zijian Zhao](https://www.researchgate.net/profile/Zijian-Zhao-11). We produce this project in our Data Security and Privacy class.

## Introduction

Location services have brought a lot of convenience to people's daily life, and nearest neighbor query as a basic service of location services is widely used in various scenarios, however, how to protect their privacy security when users use nearest neighbor services has become an important issue to be solved. Among the database query quadruplets sent by users to the LBS server, location privacy and query privacy are the two main concerns. This algorithm is based on a pseudo-location approach to solve the user's location privacy problem. In the traditional fake location approach, the user generates some dummy elements as obfuscated locations to send to the server, making it impossible for a malicious attacker to obtain the user's exact location. However, the method is not resistant to successive query attacks by attackers, i.e. there is a true location in each query, and then the results of the multiple query attacks are intersected to potentially arrive at the true location, which is a security concern of the fake location method. In addition, as the user sends multiple fake locations to the server, the server will return multiple locations, and the matching of these multiple location proximity queries will cause some storage pressure locally. The simple algorithm described in this paper therefore integrates the need for location privacy and anonymity with the user's local storage and processing matching needs, and generates dummy elements to be sent to the server for querying in order to achieve both LBS privacy and service requirements.

## Algorithm design

### Algorithm background hypothesis and metrics setting

Before the algorithm is designed, this algorithm has 2 premises and 2 indicators to consider.

**Prerequisite 1.** In this paper, the proximity query service at the server side is considered to be a query for locations within a certain distance of the target location that match the query content. As shown in Fig. 2-1, where there are two users using the LBS service, user1 and user2, both have a query range of a circle with the sending coordinates as the centre and a radius of R.

> <img src="./fig2-1.png"  div align=center />

<div align = "center">Figure 2-1 User LBS query server display</div>

**Prerequisite 2.** In order to ensure the quality of service of LBS, the result of the coordinate location query sent to the server should be able to meet the real query needs of the user. The specific situation is shown in Figure 2-2, in which it is assumed that there are three generated dummy elements, namely dummy node1, dummy node2, dummy node3. user's query range.

<img src="./fig2-2.png"  div align=center />

<div align = "center">Figure 2-2 User LBS query dummy results display</div>

**Quantifier 1.** Storage, computational pressure. This algorithm uses the query range area as a metric to measure the storage pressure. As shown in the figure, the concatenation of three dummy query ranges in Figure 2-3 can represent the query range sent from the server to the user side, i.e. the data to be processed by the user side. Therefore, the number of query data should be proportional to this area, i.e. the larger the area, the more query results. Therefore, the concatenation of query areas can be used to represent the local storage and processing pressure.

<img src="./fig2-3.png"  div align=center />		

<div align = "center">Figure 2-3 User LBS query service dummy schematic</div>

**Quantifier 2.** Privacy anonymity. This algorithm considers privacy anonymity from an attacker's perspective. Suppose a malicious LBS attacker wants to obtain the user's real location and the attacker knows the dummy generation algorithm. The attacker has access to only three (tentatively assumed) dummy elements, and the attacker wants to reverse the probability of the user's true location from the three dummy elements, based on the generation scheme of this algorithm. As shown in the figure, the red circle in the middle is the real search location of the user's demand, the black boundary circles are centered on $A,B,C$ respectively, and the intersection points between them are $X,Y,Z$ on the outside, respectively. This area is the possible range of the user's real location under these three dummy elements, and the size of this area is defined as the privacy anonymity. The larger the area of this region, the higher the privacy anonymity.

### Algorithm analysis and detailed design

The improved dummy location generation algorithm takes into account two main factors, the anonymity of the generated dummy locations and the computational and storage pressure that the query service puts on the local area. As shown in Figure 2-4, $A_{1},A_{2},A_{3}$ are three dummy elements whose query range is the circle drawn by three solid lines, and the outer intersection of the three dummy query circles are $B,C,D$ respectively



<img src="./fig2-4.png"  div align=center />

<div align = "center">Figure 2-4 User LBS query service dummy schematic</div>

As stated at the beginning of the algorithm design, the measure of privacy anonymity is the area of the inwardly concave curve enclosed by $A_{1},A_{2},A_{3}$. Let the length of $A_{1}A_{2}$ be $a$, the length of $A_{2}A_{3}$ be $b$, and the length of $A_{1}A_{3}$ be $c$. Then this area of privacy anonymity has


$$
S_{anonymous}
=S_{\Delta A_{1}A_{2}A_{3}}-S_{bowA_{1}A_{2}}-S_{bowA_{2}A_{3}}-S_{bowA_{1}A_{3}}\\
=\sqrt {p(p-a)(p-b)(p-c)}+\sum_{i \in \left \{a,b,c  \right \}} \frac{i}{2} \sqrt{R^{2}-\frac{i^2}{4}}  -\pi R^2\cdot \frac{2\arcsin\frac{i}{2R}}{2\pi}.
$$


where $P=\frac{a+b+c}{2}$ (obtained from the Hyland formula), and $R$ is the query radius set by the server. This formula has a maximum value when the circles with $B,C,D$ as centers are tangent to each other, i.e. when $a=b=c=R$.

In this case, consider the value that measures the storage, computational pressure, i.e. the concatenated area of the three circles shaved off the query area of the true position, the useless area is
$$
S_{useless}=S_{\odot A_{1}} + S_{\odot A_{2}} +S_{\odot A_{3}} - S_{\odot o}.
$$


For anonymous and useless areas, the upper and lower bounds are calculated as follows:


$$
S_{anonymous} \in \left [ 0,( \sqrt{3}-\frac{\pi}{2} )R^2  \right ], S_{useless} \in \left [ 0,( \sqrt{3}+\frac{\pi}{2} )R^2  \right ].
$$


Therefore, the function has to be parameterised by $S_{anonymous}$ and $S_{useless}$ to ensure that the two are in balance. Analyzed from a realistic point of view, the equation has the requirement that,

1. The overall consideration value should ensure that when $S_{anonymous}$ is constant, it decreases as $S_{useless}$ increases.
2. The overall consideration value is to ensure that when $S_{useless}$ is constant, it increases as $S_{anonymous}$ increases.

As the range of values of $S_{anonymous}$ and $S_{useless}$ are different, considering the possibility of large numbers covering small numbers, it is necessary to erase the influence of their actual values on the considered values. The following equation is designed in this algorithm, and when this equation is taken to the maximum, it is considered to be comprehensive and good enough to meet the requirements of privacy and anonymity and resist continuous query attacks; and to meet the requirements of reducing local storage and computational pressure. The comprehensive evaluation value equation is as follows
$$
S_{synthesis} = \frac{1}{( \sqrt{3}-\frac{\pi}{2} )R^2}\cdot S_{anonymous} - \frac{1}{( \sqrt{3}+\frac{\pi}{2} )R^2}\cdot S_{useless}.
$$

## experiment

### Results demonstration and performance analysis

Figure 4-1 shows the effect of several executions of generating dummy positions respectively, where the user real point is the red position (0,0), and in the real case the generated dummy position can be panned according to the user real position. (These are not the most advantageous, just some case demonstrations). The blue position is the generated dummy element, the yellow circle is the user's real query range, and the other black borders are the query range of the dummy element.

<center class="half">
    <img src="./fig4-11.png" width="300"/>
    <img src="./fig4-12.png" width="300"/>
    <img src="./fig4-13.png" width="300"/>
    <img src="./fig4-14.png" width="300"/>
</center>

<div align = "center">Figure 4-1 Results display</div>

The images above show some of the generated dummy elements, and Figure 4-2 below shows the values with the corresponding plots when the composite measure is taken to its maximum during the experiment, at which point the composite measure $S_{synthesis} = 0.11693531882113717$.

<img src="./fig4-2.png"  div align=center />

<div align = "center">Figure 4-2 Experimental synthesis of the effect of dummy elements at maximum value</div>

As shown in Figure 4-3, the combined set of consideration values for 1000 executions of the experiment is plotted, and as can be seen in Figure 4-3 the range of the consideration values is very close to 0, obtained by combining the computation, storage pressure and privacy anonymity. The highest point in the 1000 calculations, i.e. the discrete point with the highest Y value, was selected as the result of the dummy element at this point.

<center class="half">
    <img src="./fig4-31.png" width="300"/>
    <img src="./fig4-32.png" width="300"/>
    <img src="./fig4-33.png" width="300"/>
    <img src="./fig4-34.png" width="300"/>
</center>

<div align = "center">Figure 4-3 Experimental execution composite consideration values</div>

### Attack Analysis

​	Assuming that the attacker has access to the LBS server data, he will be able to obtain the user query and the corresponding three dummy locations. From the above algorithm, it can be seen that after the attacker obtains the three dummy positions, firstly, from "premise 1: the dummy query should cover the original query range", it can be seen that the merged area generated by the three dummy positions should completely cover the original query range, so the user's real query range circle should be within the area generated by the dummy. The set of positions of the center of the circle of the user's query within this area is the set of the user's true positions. And this set of locations is not fragmented, but is a concentrated piece of area, bounded by a red line, as shown in Figure 4-4. The larger this area is, the less the attacker can determine the exact location or range of the user. In this algorithm, this method is theoretically unattackable, i.e. the attacker cannot obtain a valid location of the user, as user privacy is taken into account in the synthesis. The continuous query attack, which uses intersection to find the exact location of the user, will also not be successful.

<img src="./fig4-4.png"  div align=center />

<div align = "center">Figure 4-4 Attacker guesses user location range map</div>

