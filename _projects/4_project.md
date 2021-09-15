---
layout: post
title: Industrial data privacy
description: Protection of Sensitive Data in Industrial Internet Based on Three-Layer Local/Fog/Cloud Storage
---

This project is my work from from March to August in 2019 , work with Changbo Yuan, [Zijian Zhao](https://www.researchgate.net/profile/Zijian-Zhao-11), Qian Su and Defan Xue, supervised by by [Prof. Yingxu Lai](http://dmslab.hkg03.bdysite.com/index.php/people/yingxu-lai/) and [LECT. Jing Liu](https://english.bjut.edu.cn/info/1152/1586.htm). We posted the work as a [patent](https://zhuanli.tianyancha.com/e63096509de4c720f019a966351dfb85) and published part of it in a [journal](https://www.hindawi.com/journals/scn/2020/2017930/).

<img src="./fig1.png"  div align=center />

Industrial Internet technology has developed rapidly, and the security of industrial data has received much attention. At present, industrial enterprises lack a safe and professional data security system. -us, industries urgently need a complete and effective data protection scheme. -is study develops a three-layer framework with local/fog/cloud storage for protecting sensitive industrial data and defines a threat model. For real-time sensitive industrial data, we use the improved local differential privacy algorithm M-RAPPOR to perturb sensitive information. We encode the desensitized data using Reed–Solomon (RS) encoding and then store them in local equipment to realize low cost, high efficiency, and intelligent data protection. For non-real-time sensitive industrial data, we adopt a cloud-fog collaborative storage scheme based on AES-RS encoding to invisibly provide multilayer protection. We adopt the optimal solution of distributed storage in local equipment and the cloud-fog collaborative storage scheme in fog nodes and cloud nodes to alleviate the storage pressure on local equipment and to improve security and recoverability. According to the defined threat model, we conduct a security analysis and prove that the proposed scheme can provide stronger data protection for sensitive data. Compared with traditional methods, this approach strengthens the protection of sensitive information and ensures real-time continuity of open data sharing. Finally, the feasibility of our scheme is validated through experimental evaluation.

