---
title: 常见机器学习算法
category: 数据分析
tags: data
---

# 常见机器学习算法

## Classification 分类

分类算法属于监督学习算法。监督学习算法表示你拥有大量的样本和正确答案。

分类算法的目的是为了找到决策边界，帮我们将数据进行分类，并用决策面来预测新的数据。
输入训练集，包括大量的特征，和正确标签，训练得到分类模型，并进行评估和预测。

三种常用的分类算法为：朴素贝叶斯、SVMs、决策树，以下是三种算法的对比。

First Header | 朴素贝叶斯 | SVMs | 决策树
------------ | ---------- | ---------- | ------------
优势 | 非常易于执行；特征空间非常大；运行非常容易；非常有效 | 支持向量机在具有复杂领域和明显分界的情况下，表现十分出色  | 测量决策树的生长情况，在适当的时间停止决策树生长非常重要。可以通过所谓的集成方法，从决策树中构建更大的分类器
缺点 | 有时会间断，无法识别组合的特征含义 | 在海量数据集中，它们的表现不太好。因为在这种训练集中，训练时间将是立方数。另外，噪音过多的情况下，效果也不好。所以，如果类严重重叠，你需要考虑独立证据，这时候朴素贝叶斯分类器会更有效| 容易过拟合，尤其是在你具有包含大量特征的数据时，复杂的决策树可能会过度拟合数据。所以你需要谨慎对待使用决策树挑选的参数，调整参数以以防过度拟合

如果你拥有海量的数据集，有很多很多的特征，直接可运行的SVMs的速度可能会很慢。数据的某些噪音，可能会导致过拟合现象。
所以，我们会在测试集上进行测试，看看它的表现如何。

### 在选择监督算法时，需要考虑哪些东西？

根据这个基本原则，可以对机器学习的算法进行选择。

1. 从执行效率上考虑
2. 从特征空间上考虑
3. 运行是否容易、有效
4. 考虑算法的缺点

后期继续总结。

## Regression 回归

### 线性回归

$Y = β0 + β1 * X1 + β2 * X2 + …… + βn * Xn + \epsilon$

使用最小二乘法来求是的误差$\epsilon^2$和最小的β0，β1，……，βn。

评估线性回归好坏的指数是 $r^2$，$r^2$ 的范围是0~1，越接近1，说明回归线拟合的越好。

## Clustering 聚类

聚类算法属于非监督算法。也就是我们拥有大量的数据，但是没有标记是否类别。
在这种情况下，所有的数据都属于一类。
我们需要根据数据的特征，把相似的数据分到一个簇里面，相异的数据分到不同的簇里面。

聚类常用于从多个维度对数据进行划分。例如，用于客户细分。

### K-means

原理是，通过对特征进行分析，找到潜在的分类，使得不同类之间距离较远，同一类之间距离都较近。从而完成数据划分。

核心算法是:

1. 设置N个中心点；
2. 通过数据到这N个中心点的距离将数据进行划分；
3. 调整中心点的位置，使得划分到同一个类里面的点，到中心点的位置最小；
4. 再根据中心点的位置对所有的数据重新划分；
5. 迭代第3步和第4步，直到不再发生变化。

K-means的问题是，过度依赖最开始设置的中心点的位置。
很可能设置同样多的中心点，并迭代同样多的次数，最后划分出来的结果并不相同。

## Dimensionality reduction 降维

当数据维度特别多时，会加重机器的运行负荷，同时会造成机器学习陷入细枝末节中。

在这种情况下，我们常常需要对数据进行降维，找到承载了大多数信息的主要特征，再将其用于真正的机器学习中。

常见的方法有主成分分析法

### 主成分分析 PCA

PCA是一套用于各类数据分析的分析方法，这些分析包括特征集压缩。
每当你的数据需要直观化的时候，你都可以采用它。

如果你收到任何形状的数据，无论是何种形状，PCA会仅通过转化和轮换发现从旧坐标系统获得的新坐标系统。

方差：在统计学上，指数据分布的大致差幅。
对于一个具有较大方差的特征，它的样本散布的数值范围极大。对于一个方差较小的特征，它的样本则是紧密聚集在一起的。

#### 主成分：
所以，根据上面的分析，我们可以知道，一个数据的主成分，就是具有最大方差的方向，如果针对很多维度的特征来说的话，就是具有最大方差的这个特征，就是主成分。

#### 为什么用最大方差的方向作为主成分？

因为它能最大程度的保留来自原始数据的信息量。使得我们在进行特征压缩时，可以保留更多的信息。

#### 第二、第三主成分

同前面的定义，我们可以将每个特征的方差进行排序，就可以得到主成分的排序了。

在机器学习中，对于特征值很多的数据集，我们通常先用主成分分析法找到最重要的特征，再使用这些特征来进行机器学习，构建我们的预测模型。

好处是，可以让机器学习过程效率提高，同时避免被细枝末节所干扰，导致模型过拟合。

#### 总结

1. PCA是将输入特征转化为其主成分的系统化方法，这些主成分之后可以供你使用，而非原始输入特征。
你将使用这些新特征用于分类和回归任务中。

2. 主成分的定义是，数据中，使方差最大化的方向，它可以在你对这些特征进行投影或压缩时，将出现信息丢失的可能性降到最低。

3. 你还可以对主成分划分等级，数据因特定主成分产生的方差越大，那么该主成分的级别越高。

4. 主成分从某种程度上来说，是垂直的，（因为每个特征都在不同的维度上）所以从数学的角度来说，不同的主成分是不可能重叠的。

5. 主成分数量是有上限的，最大值等于输入的特征量的数量。通常情况下，我们只使用最大的几个主成分。

## Model selection 模型选择

暂无相关信息。

## Preprocessing 预处理

暂无相关信息。
