---
title: 设计 AB Test 
category: 数据分析
tags: data
---

# 设计A/B 测试

在网络世界中，当你做 A/B 测试时，要谨记的一件事是，确定用户是否会喜欢这个新产品或新功能，该改进对于公司总体目标有没有用处；
所以在进行 A/B 测试时，你的目标是设计一个合理且能够给到你可复验的结果的实验，让你能够很好地决定是否要发布一款产品或功能。

#### A/B 测试的方法

一般来说，在科学领域，假设检验是确定创新的关键方法。
在A/B测试中，我们最想看到的是对照组和实验组返回一致的响应，让你能真正地决定试验的结构，确定实验组和对照组是否有很明显的差异。

#### A/B 测试的步骤

1. 提出试验假设，和希望通过实验取得的结果；
2. 选择度量指标，定义并验证指标；
3. 确定引流单元和总体
4. 确定试验规模、风险和实验时间；
5. 对结果进行完整性检验，确保一切顺利；

## 试验假设

以Udacity在线学习网站为例，
先提出假设，例如，将开始按钮从粉色改成橘色，将提高按钮的点击概率。由于最终的业务指标是课程完成率，我们还可以假设上述改进会提高终极业务指标，即完成课程的总数。

接下来，我们需要选择一个指标来测量这个变更。

## 选择度量指标

根据实验设计，我们需要选择两种指标

1. 不变指标
2. 评估指标

#### 不变指标

不变指标用于不变量检查：这些指标在实验组和对照组中都不会更改。   

我们需要对不变指标进行完整性检查，确保实验能够顺利实施。   

如果不变指标通过了完整性检查，说明实验没有受到其他非实验因素的影响，后面对于评估指标的判断是可信的。   

如果不变指标没有通过完整性检查，说明实验受到了其他因素的影响，这种情况下，我们需要找到影响实验的因素，再重新设计实验或排除该因素，直到不变指标通过完整性检查为止。


#### 评估指标

用来评估实验效果的指标。

通过该指标，比较实验组和对照组是否存在统计显著性，从而提出建议。

可以使用假设检验分析方法。

## 确定引流单元

我们要选择总体。
—— 要判定哪些是合格对象，是所有人，还是仅限于美国，还是其他？在完整性检验与评价指标计算过程中，要保证测试与指标计算，施加与同等总体。

我们要决定实验组和对照组中的实验对象是什么？
—— 总体中被选为测试对象的单元叫做分组单元，也就是引流单元。

选择实验对象是指：
—— 选择合适的引流单元，引流单元也就是分组单元。

常见的引流单元有：

1. user-id ：用户ID
2. cookie：网站自动为用户建立的
3. event：一个事件，适用于不可见的更改，不然更改对于同一个用户有可能一会儿可见，一会儿不可见，用户无法获得一致的体验
4. device ID：设备ID，只能标识移动设备，不能跨平台保持一致性
5. IP address：IP地址，用户登录时使用的网不同，IP也会不一样


引流单元的选择有以下几个条件：

1. 用户一致性。
	1. 针对可见更改或需要知道具体用户的更改，常用 user-id 和 cookie等引流单元。 
		2. user-id：保持各个设备中的一致性
		3. cookie：保持登录前后的一致性
	4. 针对不可见更改
		5. event
2. 道德问题
	3. 如果使用 user-id，需要保证安全性和用户知情权
3. 差异性
	4. 需要尽量使引流单元（分组单元）和分析单元一致。
	5. 分析单元是指指标的分母，例如：计算点击率指标时，用点击量除以页面查看量，那么页面查看量就是分析单元
	6. 如果分析单元不同于分组单元时，使用分析方法计算差异性时，会导致差异性大大增加。
	7. 原因是：用分析方法计算差异时，我们会假设数据的分布，例如假设数据符合二项分布，并假设每次事件发生是独立的，例如，每次将cookie分到实验组或者对照组这个事件是独立的。如果引流单元和分析单元都是cookie，那我们假设每次事件独立是有效的。如果引流单元为 user-id，分析单元为 cookie，那假设每次事件独立则是无效的，因为按user-id分组，它们之间实际上已经存在了某种关系，而这种关系会导致差异性大大增加。也提高了实验的风险。
 
## 计算实验规模

在实验开始前，我们需要决定采集多少实验对象，来获取统计显著性结果。

如果想发现任何有意思的东西，我们需要确保足够的功效，从而得到高概率的结果，也就是统计显著性。

功效与规模呈现负面关系。
想要探测的改变越小，或者想要的置信度越高，需要运行的实验规模就越大，也就是对照组和实验组需要更多的实验对象。


实验规模可以通过在线计算器来计算。
链接如下：
http://www.evanmiller.org/ab-testing/sample-size.html#!10.93;80;5;1.56;1

实验规模由以下几个方面决定
1. α 置信度
2. β = P(fail to reject / null false)  （通常用1-β来视为实验的敏感度，敏感度越高，越容易检测到差异。根据经验，1-β 一般设置为 80%）
3. dmin（**最小实际显著性**，也就是实验最小达到什么变化，才具有实际意义，这个值是根据经验估算出来的，需要考虑实际情况和其他成本）
4. SE标准误差

页面规模越大，标准误差越小。置信区间也就越小。

## 计算实验所需时间

这个主要是根据实验总体规模，和每天能够分配到该A/B测试的流量来定的。

主要会评估实验的风险，来确定可以投入的流量。

另外，需要考虑实验时间。如果太长的话，可能会出现其他不可控因素。一般比较合适的时间是在两周左右。

同时，对于可见的新功能改进，可以给用户留一定的探索时间。因为可能会有新奇效应。

## 评估实验风险

风险主要是从一下几个方面来评估。
1. 从身体、情感、心理方面
2. 从道德伦理方面
3. 数据库安全方面
4. 数据敏感性方面


**实验开始后，我们要按照实验设计，开始收集数据。达到预期时间后，根据数据来进行分析。**

# 实验分析

## 进行完整性（合理性）检查

合理性检查的重要性：
由于实验过程中，有太多环节可能会出现差错，导致实验结果无效，例如，实验组和对照组分配错误，或设置了不同的流量筛选条件，或设计了采集数据的功能，但实际采集到的数据并不是目标对象，或计算点击概率的方法出现了错误，等等。

所以，我们要在分析实验结果之前，对这些进行测试。

合理性检查主要是检查不变指标。主要有两种检查对象：

1. 需要检查实验组和对照组的总体规模，看是否具有可比性；
2. 需要检查实际的不变量，这类指标不随实验的进行而发生改变，而你要做的就是检测它们是否没有发生变化；

只有完成上述的完整性检查后，才能进入后续的分析阶段，判断实验是否合理，并提出建议。

### 如何进行完整性检查？

检查数据在实验组和对照组中是否有合理的相似性。

相似性是指，从统计学上来说，实验组和对照组的值没有显著性差异。

#### 检查实验组和对照组的总体规模，看是否具有可比性

假设实验以cookies为转移单元。实验每天想实验组和对照组分配各一半流量，实验时间是15天。实验组分配到的总cookies数量是61818，对照组分配到的总cookies是64454.
如何判断对照组和实验组的cookie总量的差异是否在你的预料之内？

对于这个问题，由于我们分配cookie时，会尽量保证两个组条件一致，故每条cookie进入实验组和对照组的概率是一样的，P = 0.5 
由于分到实验组还是对照组，每次分配只能有一种结果，是相对对立的，且多次分配是相互独立的，故而分到对照组的次数（或者是实验组）遵循二项分布定理。所以，可以构建一个二项式置信区间。

（二项分布：二项分布（英语：Binomial distribution）是n个独立的是/非试验中成功的次数的离散概率分布，其中每次试验的成功概率为p）

在本例中，由于总体有12万数据，已经足够假设该二项分布逼近正态分布。

1. 计算二项分布的标准差，公式为 $SE = \sqrt{p(1-p)/N}$

2. 由于 P=0.5， $SE = \sqrt{(0.5*(1-0.5)/(61818+64454))}$ = 0.0014   
3. 在α = 0.05的情况下，$m = z*SE = 1.96*0.0014 = 0.0027$
4. 分配到对照组的概率的置信区间为： (0.0473, 0.0527)

计算实际得到的对照组的概率为： P= 64454/(64454+61818) = 0.5104
不在置信区间内，故有可能是实验设置有问题。

##### 检查问题

在这种情况下，可以通过每天分配到对照组的概率来查看，是某天的数据出了问题，还是大部分出了问题，从而找到问题的原因。

只有找到了问题，解决了问题，才能进行下一步的分析。


## 效应大小检验

效应大小的评估方法：计算评估指标在实验组和对照组之间的差异的置信区间。
如果置信区间不包含 0（这就是说，你可以确信它是会变的），这个指标具有统计显著性。如果置信区间不包含实际显著性边界（这就是说，你可以确信变化对业务是有用的）。

实际显著性边界是指根据经验，估算数据发生多少改变才是有意义的。这个根据网站的体量，以及进行功能改进的成本等等来估算，找到一个合适的值。只有改进至少达到这个值，才认为实验时有效果的。

**案例基本数据如下：**

假设评估指标为总转化率，总转化率 = 总试用课程量 / 总点击量
其中
对照组：总点击量17293、总试用课程用户量3785，P1 = 3785/17293
实验组：总点击量17260、总试用课程用户量3423，P2 = 3423/17260

**则计算实验组与对照组差异的置信区间如下：**

根据上述条件可知： P1 = 0.2189, P2 = 0.1983
实验组与对照组的概率差 P(diff) = P2-P1 = -0.0206

接下来，我们通过组合概率来计算标准偏差和误差范围

组合概率： $P(pool) = (x1 + x2)/(N1 + N2) = (3785+3423)/(17293+17260) = 0.2086$

组合标准差：
SE(pool) = sqrt[p(pool)*(1-p(pool))*(1/N1 + 1/N2)]
= sqrt[0.2086*(1-2086)*(1/17293+1/17260)] = 0.0044

误差范围：
$m = z*SE(pool) = 1.96*0.0044$ = 0.0086 (α=0.05)

则置信区间为 
下限：P(diff)-m = -0.0292
上限：P(diff)+m = -0.012

由于 假设H0 是，实验组和对照组没有差异，就 d = 0, d~(0, SE(pool))
故，当 d > m 或 d < -m 时，可以拒绝零假设。由于 -0.0206 < -m ，故拒绝零假设，实验组和对照组有负的显著性差异。

由于根据经验估计的最小实际显著性是 d(min) = -0.01，而置信区间不包含 d(min), 故实验同时具有实际显著性。

## 符号检验

可以通过以下链接来进行符号检验：
http://graphpad.com/quickcalcs/binomial1.cfm

符号检验需要返回查看每天的具体数据，需要计算总天数（假设为23），和对照组大于实验组的天数（假设为19）。
由于假设是实验组和对照组相似，故我们假设对照组>实验组的概率为0.5，反之也为0.5

我们通过在线计算器，算出发生概率P-value = 0.0026
而 α = 0.05， 故而可以说小概率事件发生了，这种情况具有显著性。

如果 P-value > α ，说明不具有统计显著性。

# 实验结果

查看分析的结果与预期结果是否一致，再根据结果来评估实验是否可行

# 建议

给出建议。

