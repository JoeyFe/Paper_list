Secure, privacy-preserving and federated machine learning in medical imaging
===

为了防止损害患者隐私，同时促进旨在改善患者护理的大型数据集的科学研究，需要通过技术解决方案同时满足对数据保护和利用的需求。在这里，作者概述了用于联邦、安全和隐私保护的人工智能的当前和下一代方法，重点是医学成像应用，以及潜在的攻击媒介以及医学成像及其他方面的未来前景。

> 攻击方式：
重识别（id归属）攻击，重构数据集攻击，追踪攻击，投毒攻击，模型繁衍重构
> 防御方式：
从设计系统之初的每一步保护隐私，匿名化，假名化，安全AI（保护模型），隐私AI（保护输入输出），联邦学习，差分隐私，同态加密，安全多方计算，硬件层面保护。

![image](https://user-images.githubusercontent.com/65484555/129478410-5bd092ea-9e4b-43f3-a72d-a6e703f1bd8e.png)

![image](https://user-images.githubusercontent.com/65484555/129478411-1cfc1954-5acf-453c-9379-500f90218f12.png)

> 综述文章，主要是对运用的隐私保护技术进行了总结归纳，提出了10点前景。

1.采用分散数据存储和联邦学习系统，取代当前的数据共享和集中存储。给了几篇医学相关的论文。
2.克服已经提出的个别技术的缺点，有效的加密和隐私原语，传输策略。
3.需要研究在准确性、可解释性、公平性、偏见和隐私（隐私-效用的权衡）之间的权衡。例如，在放射学领域，加密设置中的可解释性仅限于对新图像评估训练算法或检查纯文本输入数据；然而，中间输出可能会模糊，难以解释。目前关于可解释的研究可以缓解这一问题。
4.设计和实施安全和高效的系统，不仅抵抗（或至少揭示）由于技术实施造成的错误，而且能够对抗试图破坏系统的半诚实或不诚实的参与者/对手。
5.监控已部署的模型，即使纠正
6.参与方取消训练
7.开源工具和框架
8.开发可审计和客观可信的系统（即不依赖主观断言--例如政府）将促进个人和决策者普遍接受安全和私人人工智能解决方案。
9.安全和私人人工智能解决方案提供保护隐私的技术能力，以及量化和跟踪单个数据集关于算法性能的附加值的新技术，将增强私人数据作为当前经历供应过剩的进化数据经济中稀缺和有价值资源的概念
10.加强病人的教育、医生、研究人员和政策制定者和开放科学、公共和政治的合作，加强隐私的文化价值和培养可持续的信任和科学和社会价值一致的合作
