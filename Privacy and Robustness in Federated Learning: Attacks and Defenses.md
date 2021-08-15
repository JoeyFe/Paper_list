Privacy and Robustness in Federated Learning: Attacks and Defenses
=
Lingjuan Lyu∗ , Han Yu∗ , Xingjun Ma, Lichao Sun, Jun Zhao, Qiang Yang∗, Fellow, IEEE, and Philip S. Yu, Fellow, IEEE.
***
**摘要**:随着数据越来越多地存储在不同的地方中，而社会也越来越意识到数据隐私问题，传统的人工智能（人工智能）模型的集中训练正面临着效率和隐私方面的挑战。最近，联邦学习(FL)已经成为一种替代的解决方案，并继续在实际应用场景中蓬勃发展。现有的研究证明现在的FL协议容易受到系统内部或外部对手的攻击，损害数据隐私和系统的鲁棒性。除了训练强大的全局模型外，设计具有隐私保障并对不同类型对手具有抵抗力的FL系统是至关重要的。在本文中，我们对这个问题进行了第一次全面的调查讨论。通过对FL概念的简要介绍，设计一个独特的分类方法涵盖：1)威胁模型（threat models）；2)中毒攻击和健壮性防御（poisoning attacks and defenses against robustness）；3)推理攻击和隐私防御（inference attacks and defenses against privacy），我们对这个重要主题进行讨论回顾。我们强调了各种攻击和防御所采用的直觉、关键技术和基本假设。最后，我们讨论了面向健壮和隐私保护的联邦学习的未来研究方向。
## 1、introduction
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

![image](https://user-images.githubusercontent.com/65484555/129474506-02237c48-219e-4178-881f-da7c9cd78f38.png)

### 1.4 Secure FL
隐私泄露保护的方法：同态加密、安全多方计算、差分隐私。同态加密和安全多方计算通信计算开销大，差分隐私导致恶意竞争 可以用 Distributed Differential Privacy (DDP)解决

`模型鲁棒性保护：由于梯度只在服务器端可见，通用的集中机器学习的方法无法运用到联邦学习中，该防御方法必须对数据中毒和模型中毒攻击（如拜占庭攻击、后门攻击和西比尔攻击）都具有鲁棒性。`
> G. Damaskinos, E. M. El Mhamdi, R. Guerraoui, A. H. A. Guirguis, and S. L. A. Rouault, “Aggregathor: Byzantine machine
learning via robust gradient aggregation,” in SysML, 2019.

![image](https://user-images.githubusercontent.com/65484555/129474663-77e0c595-d4ff-4100-af8a-449417b296b3.png)

## 2、THREAT MODELS
### 2.1 Insider v.s. Outsider
内部攻击（由参与方或服务器方发起）
1、拜占庭式：拜占庭式机器不需要遵守协议，可以向服务器发送任意消息；特别是，他们可能精通系统和学习算法，并可以相互串通
>[13]P. Blanchard, R. Guerraoui, J. Stainer et al., “Machine learning with adversaries: Byzantine tolerant gradient descent,” in NeurIPS, 2017, pp. 119–129
[14]D. Yin, Y. Chen, K. Ramchandran, and P. Bartlett, “Byzantinerobust distributed learning: Towards optimal statistical rates,”CoRR, arXiv:1803.01498, 2018.
[47]Y. Chen, L. Su, and J. Xu, “Distributed statistical machine learning in adversarial settings: Byzantine gradient descent,” Proceedings of the ACM on Measurement and Analysis of Computing Systems, vol. 1, no. 2, p. 44, 2017
[50]L. Chen, H. Wang, Z. Charles, and D. Papailiopoulos, “Draco: Byzantine-resilient distributed training via redundant gradients,”CoRR, arXiv:1803.09877, 2018.

2、西比尔：FL系统中的西比尔对手可以模拟多个虚拟参与者帐户，或选择以前受损的参与者，对全局模型[26]，[28]发起更强大的攻击。
### 2.2 Semi-honest v.s. Malicious
半诚实：不违反FL的基本协议，只能观察接收到的信息
恶意：并通过修改、重放或删除信息来任意偏离FL协议
### 2.3 Training Phase v.s. Inference Phase 
训练阶段：损害训练数据集和模型完整性
推理阶段：不目标模型，欺骗模型产生错误的预测（有针对性/非目标性），收集关于模型特征的证据

## 3 POISONING ATTACKS 

根据攻击者的目标，中毒攻击可分为两类：
a)非目标中毒攻击[55]，[57]，[58]，[59]，[60]
b)靶向中毒攻击[26]，[27]，[61]，[62]，[63]，[64]，[65]，[66]。学习到的模型输出对手为特定测试示例指定的目标标签，例如，预测垃圾邮件为非垃圾邮件

### 3.1 Data Poisoning
数据中毒（能否改变训练数据的标签）分为
1. 干净标签
2. 脏标签 a）标签翻转label-flipping attack（改变一部分标签）b）后门中毒backdoor poisoning 修改原始训练数据集的单个特征或小区域，以在模型中植入一个后门触发器。该模型在干净的数据上表现正常，但每当触发器（例如，图像上的邮票）出现时，它就会不断预测目标类。
最近的一项工作表明，中毒边缘情况（低概率）训练样本是更有效的（是否有对抗学习的味道）
> [24] H. Wang, K. Sreenivasan, S. Rajput, H. Vishwakarma, S. Agarwal,J.-y. Sohn, K. Lee, and D. Papailiopoulos, “Attack of the tails: Yes, you really can backdoor federated learning,” NeurIPS, 2020.

### 3.2 Model Poisoning 
这些攻击在本地模型更新上传到服务器之前[26]，[71]。

拜占庭攻击是一种非目标的模型中毒攻击，它将任意恶意的模型更新上传到服务器，从而导致全局模型的故障。

`Byzantine-robust federated learning methods([13])`

![image](https://user-images.githubusercontent.com/65484555/129475123-f98bddec-d294-43ee-a467-d2f62aa8d7fa.png)

>[13] P. Blanchard, R. Guerraoui, J. Stainer et al., “Machine learning with adversaries: Byzantine tolerant gradient descent,” in NeurIPS, 2017, pp. 119–129.
[30] J. Bernstein, J. Zhao, K. Azizzadenesheli, and A. Anandkumar,“signSGD with majority vote is communication efficient and byzantine fault tolerant,”in In Seventh International Conference on Learning Representations (ICLR), 2019.
[46] G. Damaskinos, E. M. El Mhamdi, R. Guerraoui, A. H. A. Guirguis, and S. L. A. Rouault, “Aggregathor: Byzantine machine
learning via robust gradient aggregation,” in SysML, 2019.
[60] C. Xie, O. Koyejo, and I. Gupta, “Fall of empires: Breaking byzantine-tolerant sgd by inner product manipulation,” in UAI.PMLR, 2020, pp. 261–270.
[71] L. Lamport, R. Shostak, and M. Pease, “The byzantine generals problem,” ACM Transactions on Programming Languages and Systems (TOPLAS), vol. 4, no. 3, pp. 382–401, 1982.

后门攻击是一种有针对性的模型中毒攻击，旨在将后门触发器注入全局模型，而不影响其对主任务[26]、[27]、[28]、[29]的性能。触发器与一个子任务相关联，在其中对手可以控制模型以不断预测目标类[27]。
>[26]E. Bagdasaryan, A. Veit, Y. Hua, D. Estrin, and V. Shmatikov,“How to backdoor federated learning,” CoRR, arXiv:1807.00459, 2018.
[55]M. Fang, X. Cao, J. Jia, and N. Gong, “Local model poisoning attacks to byzantine-robust federated learning,” in 29th {USENIX} Security Symposium ({USENIX} Security 20), 2020, pp. 1605–1622.

## 4 INFERENCE ATTACKS
从梯度中推理隐私数据
[19], [20], [73], [74], [75]

### 4.2 Inferring Membership
给定一个精确的数据点，成员推理攻击的目的是确定它是否用于训练模型[80]。
### 4.3 Inferring Properties 
具有正确标记为目标属性的辅助训练数据，推断其他参与者的训练数据[19]的某些属性
### 4.4 Inferring Training Inputs and Labels
>[20] L. Zhu, Z. Liu, and S. Han, “Deep leakage from gradients,” in NeurIPS, 2019, pp. 14 747–14 756.

从梯度中提取深度泄漏(DLG)提出了一种优化算法，可以在几次迭代中同时提取训练输入和标签。
>[23] B. Zhao, K. R. Mopuri, and H. Bilen, “idlg: Improved deep leakage from gradients,” CoRR, arXiv:2001.02610, 2020.

提出了一种称为改进梯度深度泄漏(iDLG)的分析方法，基于共享梯度提取标签，并探索标签与梯度符号之间的相关性

## 5 PRIVACY-FOCUSED FL DEFENSE 

### 1、同态加密
比较有名的RSA [100], El Gamal [93], Paillier [92]
讲了一些用同态加密保护分布式机器学习的方法
### 2、安全多方计算
>[91] P. Mohassel and Y. Zhang, “Secureml: A system for scalable privacy-preserving machine learning,” in SP, 2017, pp. 19–38.

一般来说，SMC技术确保了高水平的隐私和准确性，而牺牲了较高的计算和通信开销，从而不利于吸引参与。基于SMC的方案面临的另一个主要挑战是要求在整个培训过程中同时协调所有参与者。这种多方交互模型在实际设置中可能不可取，特别是在联合学习设置中常见的参与者-服务器体系结构下。此外，基于smc的协议可以使多个参与者能够协作计算一个商定的函数，而不泄露任何参与者的输入信息，除了可以从计算[101]，[102]的结果中推断出的信息。因此，SMC不能保证对信息泄漏的保护，这需要在多方协议中加入额外的差异隐私技术，以解决[103]、[104]、[105]、[106]等问题

同态加密或基于smc的方法可能不适用于大规模的FL场景，因为它们会产生大量额外的通信和计算成本，对于目标学习算法中的每个操作，都需要仔细设计和实现基于加密的技术。这为恶意参与者的攻击留下了空间。例如，恶意参与者可以在全局模型中引入后门，而不被检测到。

### 3、差分隐私（这篇文章好像比较推荐）

Centralized Differential Privacy (CDP) 集中化差分隐私：由服务器端做差分隐私→一定需要一个受信任的中心服务器
Local Differential Privacy (LDP)局部差异隐私：数据所有者（参与方）在本地做差分隐私  →会导致模型效果下降
Distributed Differential Privacy (DDP)分布式差分隐私：可以说是取每个参与方做差分隐私的参数，学习他的分布学到一个代表所有参与方差分隐私的参数，（具体要看论文）

## 6 ROBUSTNESS-FOCUSED FL DEFENSE 
### 6.1 Byzantine Robustness 
对于拜占庭 Byzantine-resilient aggregation，如果高达50%的参与者在对抗时收敛是鲁棒的，则为拜占庭容错[13]

具体实践
* AUROR：
>[127]S. Shen, S. Tople, and P. Saxena, “Auror: defending against poisoning attacks in collaborative deep learning systems,” in Proceedings of the 32nd Annual Conference on Computer Security Applications. ACM, 2016, pp. 508–519.
>引入了一种名为AUROR的统计机制来在生成准确模型的同时检测恶意用户。AUROR基于这样的观察：来自大多数诚实用户的指示性特征（最重要的模型特征）将表现出类似的分布，而来自恶意用户的特征将表现出异常分布。然后，它使用k-means在训练轮中集群参与者的更新，并丢弃异常值，即来自超过阈值距离的小集群的贡献被删除。


* Krum：（被证实对于非目标攻击是无效的）
>[13]P. Blanchard, R. Guerraoui, J. Stainer et al., “Machine learning with adversaries: Byzantine tolerant gradient descent,” in NeurIPS, 2017, pp. 119–129.
>对模型离平均参与者贡献最远的前f贡献从聚合中移除。Krum使用欧几里得距离来确定应该删除哪些梯度贡献，理论上可以承受参与者池中高达33%的对手的中毒攻击

* Coordinate-wise median
>[14]D. Yin, Y. Chen, K. Ramchandran, and P. Bartlett, “Byzantinerobust distributed learning: Towards optimal statistical rates,” CoRR, arXiv:1803.01498, 2018.
>相比krum用坐标系中位数替换加权算术平均值

* Bulyan：
>[128]E. M. E. Mhamdi, R. Guerraoui, and S. Rouault, “The hidden vulnerability of distributed learning in byzantium,” CoRR,arXiv:1802.07927, 2018.
>Krum+修剪中位数

* RFA:
>[28]K. Pillutla, S. M. Kakade, and Z. Harchaoui, “Robust aggregation for federated learning,” arXiv preprint arXiv:1912.13445, 2019.
>相比krum用近似的几何中值替换加权算术平均值

* RONI：
>[133]M. Barreno, B. Nelson, A. D. Joseph, and J. D. Tygar, “The security of machine learning,” Machine Learning, vol. 81, no. 2, pp. 121–148, 2010.
>基于错误率的拒绝率（ERR

* TRIM：
>[59]M. Jagielski, A. Oprea, B. Biggio, C. Liu, C. Nita-Rotaru, andB. Li, “Manipulating machine learning: Poisoning attacks andcountermeasures for regression learning,” in SP, 2018, pp. 19–35.
>基于损失函数的拒绝(LFR)

* DRACO:
>[50]L. Chen, H. Wang, Z. Charles, and D. Papailiopoulos, “Draco: Byzantine-resilient distributed training via redundant gradients,”CoRR, arXiv:1803.09877, 2018.
>一个通过算法冗余实现的鲁棒分布式训练框架。Draco对任意恶意计算节点具有鲁棒性，同时比最先进的鲁棒分布式系统快几个数量级。然而，德拉科假设每个参与者都可以访问其他参与者的数据，这限制了其在FL中的适用性

* SIGNSGD：
>[30] J. Bernstein, J. Zhao, K. Azizzadenesheli, and A. Anandkumar,“signSGD with majority vote is communication efficient and byzantine fault tolerant,” in In Seventh International Conference on Learning Representations (ICLR), 2019.
>与多数投票相结合，使参与者能够上传其梯度的元素符号，以抵御三种半“盲”的拜占庭敌人：(i)任意调整随机梯度估计的对手；(ii)随机分配随机梯度每个坐标的符号；(iii)反转其随机梯度估计的对手。

### 6.2 Sybil Robustness 
提到一个FoolsGold方法,看这篇文章的表述看的不是很明白
>[28] C. Fung, C. J. Yoon, and I. Beschastnikh, “Mitigating sybils in federated learning poisoning,” CoRR, arXiv:1808.04866, 2018.

## 7 DISCUSSIONS AND PROMISING DIRECTIONS 

研究方向：
* 维度问题：具有高维参数向量的大型模型特别容易受到隐私和安全攻击的。大多数FL算法都需要用全局模型覆盖局部模型参数。这使得它们容易受到中毒攻击，因为对手可以在不被检测到的高维模型的情况下进行微小但具有破坏性的变化
* 当前攻击的弱点：目前主要基于GAN和DLG（BFGS）在更有效的方式和更实际的设置下攻击FL系统仍然在很大程度上未被探索。（GAN攻击假设给定类的整个训练语料库来自单个参与者，并且只有在所有类成员相似的特殊情况下，GAN构建的代表与训练数据[78]相似）
* 对免费乘车的参与者造成的漏洞：有想要白嫖全局模型的
* 具有异构架构的更多可能性：将现有的攻击和防御推广到异构的FL后，隐私保护技术和防御机制是否可以适应于具有异构架构的FL
* 对垂直联邦学习的威胁：可能只有一个参与者拥有给定学习任务的标签。在这种情况下，参与者可能有不同的可访问性或能力来攻击FL模型。对于HFL中的现有威胁是否在VFL中仍然有效，或者在VFL中是否存在新的威胁，
*  分散化的联邦学习：没有中心服务器的联邦学习的隐私保护
* 当前隐私保护技术的弱点：对抗训练能否帮助提高联邦学习的鲁棒性（主要是由于联邦学习的数据不一定是独立同分布的）、能否减小差分隐私对模型精度的影响
* 优化防御机制部署：当部署防御机制以检查是否有对手攻击FL系统时，FL服务器将需要额外的计算成本。此外，不同类型的防御机制可能对不同的攻击有不同的效果，并产生不同的成本。研究如何优化部署防御机制或宣布威慑措施的时机是很重要的。博弈论研究有望解决这一挑战。
* 同时实现多个目标：（1)快速算法收敛；(2)良好的世代 警报性能；(3)通信效率；(4)容错；(5)隐私保护；以及(6）针对有针对性、无目标中毒攻击和搭便车者的健壮性 （可以当作评价指标[140]，[141]同时解决了协作 的公平和隐私；[132]提出了一个健壮和公平的联邦学习(RFFL)框架来解决协作公平和拜占庭的鲁棒性）
##8 CONCLUSIONS
关于FL的全球合作
[www.federated-learning.org](www.federated-learning.org)



