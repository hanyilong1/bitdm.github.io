---
layout: page
mathjax: true
permalink: /2017/projects/p06/midterm/
---

# 用户行为预测 
### 小组成员
- 赵　颖 2620160012
- 王晓媛 2620160007
- 李昱燃 2620160009
## 1、概述
我们欲分三步解决实验提出的问题：数据预处理，分类算法的选择，分类算法的实现。首先，对已有的10000条数据进行预处理，选择合适的特征变量，方便分类器的训练，我们使用java编程实现了这一过程。其次，出于提高准确率、加快训练速度的目的，需要选择适当的分类算法，最终确定了随机森林、与AdaBoost结合的决策树、梯度提升决策树三种算法。最后，实现分类算法并进行分类器的训练，这一步骤还未完成。
## 2、项目进展
### 实验环境
JDK+eclipse：用java语言进行数据预处理和特征选取。
Python：用数据挖掘中常用的python进行训练、分类和预测。
### 数据预处理
给定的训练集共10000条数据，每条数据分别包括230个特征值，特征值的前190个为数值类型，后40个为string字符串类型，特征值之间以逗号（,）分隔，无特征值时为空（” ”）。
从230个特征值中选择特征值出现次数最多，较为完整的40余特征值进行训练，其余数据由于完整度不够被删去。选择特征值的方法如下：
1) 使用java编写程序，从train.txt中按行读入数据，每行记为lineTxt，由于数据之间严格采用“，”分隔，故可调用函数split()，得到tempArray数组，其元素为字符串类型，其长度为230，其中的值为空或为某一特征值。
2) 定义全局变量sum数组用于统计每个特征值的缺失次数，sum为int[230]类型，初始值皆为0，对tempArray数组中的元素逐个进行判断，若tempArray[i]值为空，则令sum[i]加1，否则不变。
3) 统计结束后，为了在获得其中缺失次数的信息的同时保存其所在列的信息，将数组复制到另一数组s中，对s进行排序，调用Arrays.sort(s)函数并输出，对输出数据进行观察统计，可得到下图结果：

![](https://github.com/gezizuozuo/bitdm.github.io/blob/master/2017/projects/P06/images/%E5%9B%BE1%E6%95%B0%E7%BB%84s%E7%9A%84%E6%A0%87%E5%8F%B7%E4%B8%8E%E5%AF%B9%E5%BA%94%E5%80%BC.png)
                           
                           图1 数组s的标号与对应值
4) 由图中统计数字不难发现，在缺失次数超过1500次后，缺失次数过多，且急剧增长，不适合用于分类器的训练，因此仅考虑缺失次数不超过1500次的特征值所在列，在限定缺失次数不超过1500次的情况下对sum数组再次进行遍历，从而得到缺失次数较少的特征值所在列。结果如下（数字表示列号）：
[5,6,12,20,21,23,24,27,34,37,43,56,64,71,72,73,75,77,80,82,84,93,108,111,112,118,122,124,125,131,132,133,139,142,143,148,152,159,162,172,180]。
### 算法选择
首先对实验中数据集的特性进行了分析。在使用的数据集中，训练数据和测试数据各10000个，数量比较大；而且该数据集中的230个特征变量并不是同一类型的，而是190个数值型变量和40个类别型变量的组合；而且数据集中有大量数据缺失。而后分析了竞赛中选手们选用的算法。参赛者使用最多的几种分类算法降序排列如下：决策树集合类的分类算法（包括随机森林、与AdaBoost结合的决策树算法、梯度提升决策树等算法）、线性分类算法（特别是逻辑回归算法）、支持向量机。可见这几种算法对于该数据集的处理有一定优势。同时，结合决策树集合分类算法的几个优势：在大数据集上的表现良好，运行速度快；处理不同类型的变量比较容易；有大比例的数据缺失时，也能保持较高的准确度；实现简单、鲁棒性好。我们最终选择了与AdaBoost结合的决策树、梯度提升决策树、随机森林三种算法进行实验。
## 3、待完成的工作
之后，我们将完成分类算法的实现工作。基于所选的梯度提升决策树、与AdaBoost结合的决策树、随机森林三种算法，由训练数据生成对应的分类器，用测试集分别对客户的忠诚度、消费欲和增值服务倾向性做出二元判别，并计算各分类器的准确率，最后将各个结果进行比较分析。

