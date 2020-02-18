neural architecture search,a _gradient-based_ method for finding good architectures.

该方法的提出基于我们观察到的现象，那就是神经网络的结构和连接度可以表示成一个可变长字符串。因此，就有可能用递归网络来生成这个字符串。

用一个控制器controller来生成神经网络的超参数。假设仅用卷积层来预测前馈神经网络，controller生成超参数，也就是一串令牌token。

**概述**
超参数包括：filter height,filter width,stride height,stride width,number of filters.每一层都会预测这几个参数。每个预测通过softmax分类器，作为下一步的输入。

controller RNN的参数是 θ<sub>c</sub>，优化的目标是最大化期望验证精度。


**利用REINFORCE训练**

[REINFORCE](http://neuro.bstu.by/ai/To-dom/My_research/Papers-2.1-done/RRNN/1/Ref/williams-92.pdf)是

REward Increment = Nonnegative Factor x Offset Reinforcement x Characteristic Eligibility

_J_(_θ_<sub>c</sub>)=E<sub>P(α<sub>1:T</sub>;θ<sub>c</sub>)</sub>[_R_]

R不可微，为了更新 _θ_<sub>c</sub>，我们采用[williams,1992](https://cloud.tencent.com/developer/article/1361122)提出的强化方法及其近似。
公式分别为

![origin](https://github.com/willhelm-nudt/photo/blob/master/williams92.png)

![approximate](https://github.com/willhelm-nudt/photo/blob/master/approx.png)

上述公式是一个无偏估计，但是方差太大，因此加入一个b，前一个结构精度的指数滑动平均。

![approximate1](https://github.com/willhelm-nudt/photo/blob/master/approx1.png)

为了加速训练过程，需要并行处理以及异步更新。

为了扩大搜索空间，让controller允许跳过连接或者层分支branching layers.为了预测连接情况，引入一种注意力机制attention mechanism，叫做[set-selection type attention](https://arxiv.org/abs/1511.04834),在第N层，增加一个锚点，包含N-1 content-based sigmoids来表示与之相连的层。sigmoid函数如下：

P(Layer j is an input layer i)=sigmoid(v<sup>T tanh(W<sub>prev<\sub>*h<sub>j<\sub>+W<sub>curr<\sub>*h<sub>i<\sub>))


```
[williams 1992]Simple statistical gradient-following algorithm for connectionist reinforcement learning.
```

