neural architecture search,a _gradient-based_ method for finding good architectures.

该方法的提出基于我们观察到的现象，那就是神经网络的结构和连接度可以表示成一个可变长字符串。因此，就有可能用递归网络来生成这个字符串。

用一个控制器controller来生成神经网络的超参数。假设仅用卷积层来预测前馈神经网络，controller生成超参数，也就是一串令牌token。

**概述**
超参数包括：filter height,filter width,stride height,stride width,number of filters.每一层都会预测这几个参数。每个预测通过softmax分类器，作为下一步的输入。

controller RNN的参数是 θ<sub>c</sub>，优化的目标是最大化期望验证精度。


**强化训练**

_J_(_θ_<sub>c<sub>)=E<sub>P(α<sub>1:T<sub>;θ<sub>c<sub>)<sub>[_R_]
