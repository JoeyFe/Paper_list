Privacy and Robustness in Federated Learning: Attacks and Defenses
=
Lingjuan Lyu∗ , Han Yu∗ , Xingjun Ma, Lichao Sun, Jun Zhao, Qiang Yang∗, Fellow, IEEE, and Philip S. Yu, Fellow, IEEE.
***
**摘要**:随着数据越来越多地存储在不同的地方中，而社会也越来越意识到数据隐私问题，传统的人工智能（人工智能）模型的集中训练正面临着效率和隐私方面的挑战。最近，联邦学习(FL)已经成为一种替代的解决方案，并继续在实际应用场景中蓬勃发展。现有的研究证明现在的FL协议容易受到系统内部或外部对手的攻击，损害数据隐私和系统的鲁棒性。除了训练强大的全局模型外，设计具有隐私保障并对不同类型对手具有抵抗力的FL系统是至关重要的。在本文中，我们对这个问题进行了第一次全面的调查讨论。通过对FL概念的简要介绍，设计一个独特的分类方法涵盖：1)威胁模型（threat models）；2)中毒攻击和健壮性防御（poisoning attacks and defenses against robustness）；3)推理攻击和隐私防御（inference attacks and defenses against privacy），我们对这个重要主题进行讨论回顾。我们强调了各种攻击和防御所采用的直觉、关键技术和基本假设。最后，我们讨论了面向健壮和隐私保护的联邦学习的未来研究方向。
## introduction
传统集中式机器学习存在通信成本、通信延迟、隐私问题所以在当今研究不可行，联邦学习将模型训练分配到数据来源的设备上，成为一个很有前途的替代ML范式。
### 1.1  Types of Federated Learning
水平联邦学习、纵向联邦学习、联邦迁移学习
其中水平联邦学分为： HFL to businesses (H2B) 和 HFL to consumers (H2C)
![image](https://user-images.githubusercontent.com/65484555/129474323-74fcefb1-de7a-4e3d-a0c8-9b9867585f68.png)

目前没有针对联邦迁移学习的攻防研究。
### 1.2 Sharing Methods in FL
**FL with Homogeneous Architectures（具有相同结构的联邦学习）：**
优化目标：
两种更新梯度策略：
FedSGD：子模型完成每次SGD，更新主模型
FedAvg：子模型在本地完成多次SGD后，更新主模型
**FL with Heterogeneous Architectures（具有不同结构的联邦学习）：**
可以消除了在传统的联邦学习[16]，[17]中发生白盒推理攻击的风险
 Federated Model Distillation (FedMD)联邦模型蒸馏（可以看一下）：
> D. Li and J. Wang, “Fedmd: Heterogenous federated learning via model distillation,” arXiv preprint arXiv:1910.03581, 2019.
### 1.3 Threats to FL
主要有可能受到的攻击：
（1）恶意服务器的目的是从随着时间的个别更新中推断敏感信息，篡改训练过程或控制参与者对全局参数的获取；
（2）对抗参与者推断其他参与者的敏感信息，篡改全局聚合参数或毒害全局模型

隐私泄露：主要是通过观察梯度进行攻击。

鲁棒性：投毒攻击（数据投毒、梯度投毒）来攻击全局模型的收敛性。
其中投毒攻击分为：
1、拜占庭攻击 Byzantine attacks 破坏全局模型的敛散性和性能。（看具体论文）
> P. Blanchard, R. Guerraoui, J. Stainer et al., “Machine learning with adversaries: Byzantine tolerant gradient descent,” in NeurIPS, 2017, pp. 119–129

> J. Bernstein, J. Zhao, K. Azizzadenesheli, and A. Anandkumar,signSGD with majority vote is communication efficient and byzantine fault tolerant,” in In Seventh International Conference on Learning Representations (ICLR), 2019.
2、后门攻击 backdoor attacks 在全局模型中植入一个后门触发器，从而欺骗模型不断预测子任务上的敌对类，同时在主任务[26]，[27]上保持良好的性能。
隐私泄露攻击和鲁棒性攻击类型及目标归纳



