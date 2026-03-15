# AI CheatSheet | AI

所谓 AI，即能够感知（Aware/Sense），然后做出决策（Decision），并且对于环境做出反应（Act）。

机器学习的目标是让机器能够自动根据数据分析预测我们想要的结果。　　机器学习有时会和人工智能（AI）混淆。但严格来讲，机器学习只是人工智能的子域。机器学习有许多不同的形式，涉及许多不同的名字：模式识别、统计建模、数据挖掘、知识发现、预测分析、数据科学、适应系统、自组织系统等。

人工智能，与机器学习的思维模式，不同于软件工程中以逻辑与数学思维去思考，以断言来证明程序各属性的正确性，并且最终得到确定性产品的开发思维模式；它的关注点从数学科学转移到自然科学，观察不确定的未知世界，开展实验，并使用统计信息 而非逻辑来分析实验结果。

佩德罗·多明戈斯在《终极算法》一书中将机器学习领域划分了五大思想学派（符号学派、联结学派、进化学派、贝叶斯学派和类推学派）。

深度学习是机器学习中使用深度神经网络的的子领域。用机器学习解决一个问题的时候，首先我们拿到一个数据，比如说这个数据对象是个图像，然后我们就用很多特征把它描述出来，比如说颜色、纹理等等。这些特征都是我们人类专家通过手工来设计的，表达出来之后我们再去进行学习。而今天我们有了深度学习之后，现在不再需要手工去设计特征了。你把数据从一端扔进去，模型从另外一端就出来了，中间所有的特征完全可以通过学习自己来解决。所以这就是我们所谓的特征学习，或者说表示学习。这和以往的机器学习技术相比可以说是一个很大的进步。我们不再需要依赖人类专家去设计特征了。

表示学习最关键的又是什么呢？我们现在有这么一个答案，就是逐层的处理。第一，我们要有逐层的处理；第二，我们要有特征的内部变换；第三，我们要有足够的模型复杂度。

AI 从感知层大致分为两大块，一块是计算机视觉，这一块已经比较成熟，无论是人脸识别、物体检测、运动检测都已经能用于实际场景中。另一块则是 NLP，虽然微软、Google 等宣称它们的 AI 翻译准确率已经极高，但实际上仍然不太好用，而多轮会话的问题没有解决，Chatbot 还是难以与人展开正常对话。

## 意义与应用

首先，它会为您提供一个可缩短编程时间的工具。假设我想编写一个程序来纠正拼写错误。我可以通过大量示例和经验法则（例如，I 位于 E 之前，但出现在 C 之后时例外），取得一定的进展，然后经过数周的努力，编写出一个合理的程序。

其次，借助机器学习，您可以自定义自己的产品，使其更适合特定的用户群体。假设我手动编写了一个英文拼写纠正程序，这个程序很成功，因此我打算 针对 100 种最常用语言提供相应的版本。这样一来，每种语言版本几乎都需要从头开始，这将需要付出数年的努力。但如果我使用机器学习技术构建该程序，然后迁移到其他语言，基本上就相当于，我只需收集该特定语言的数据，并将这些数据提供给完全一样的机器学习模型即可。

第三，借助机器学习，您可以解决自己作为编程人员不知道如何用人工方法解决的问题。作为人类，我可以认出朋友的面孔，理解他们所说的话，但所有这些都是在潜意识下完成的，如果让我编写一个程序来做这些事，我会完全不知所措。但是，机器学习算法对此却很擅长；我不需要告诉算法应该怎么做，只需向其展示大量样本，问题就可以迎刃而解。

## 发展与变迁

人工智能发展有三个阶段：计算智能、感知智能和认知智能。

第一阶段的计算智能即快速计算和记忆存储，像机器人战胜围棋大师，靠的就是超强的记忆能力和运算速度。人脑的逻辑能力再强大，也敌不过人工智能每天和自己下几百盘棋，通过强大的计算能力对十几步后的结果做出预测，从这一角度来说，人工智能多次战败世界级围棋选手，足以证明这一领域发展之成熟。

第二阶段的感知智能，即让机器拥有视觉、听觉、触觉等感知能力。自动驾驶汽车做的就是这一方面的研究，使机器通过传感器对周围的环境进行感知和处理，从而实现自动驾驶。感知智能方面的技术目前发展比较成熟的领域有语音识别和图像识别，比如做安全领域人脸识别技术的 Face++，以成熟的计算机视觉技术深耕电商、短视频等领域的 Yi+，能够对多种语言进行准确识别翻译的科大讯飞等。

第三阶段的认知智能与前面在人工智能的 3 大分支里提到的认知 AI 类似，就是让机器拥有自己的认知，能理解会思考。认知智能是目前机器和人差距最大的领域，因为这不仅涉及逻辑和技术，还涉及心理学、哲学和语言学等学科。

# 知识领域

## Mathematics | 数学基础

## Machine Learning | 机器学习

Maximum Objective Function

常见机器学习的任务可以分解为以下七个步骤：

Data Collection

Data Preparation

Build Model

Train Model

Evaluation

Tune

Predict

## Deep Learning | 深度学习

![image](https://user-images.githubusercontent.com/5803001/43595548-846b86e0-96af-11e8-951b-ae913482c19c.png)

传统的机器学习往往需要大量的领域知识与计算时间，而深度学习为我们带来了无限灵活的函数、通用的参数拟合、高速可扩展等特性的算法。

Traditional statistical models do very well on structured data, i.e. tabular data, but have notoriously struggled with unstructured data like images, audio, and natural language. Neural networks that contain many layers of neurons embody the research that is popularly called Deep Learning. The key insight and property of deep neural networks that make them suitable for modeling unstructured data is that complex data, like images, generally have many layers of unique features that are composed to produce the data. As a classic example: images have edges which form the basis for textures, textures form the basis for simple objects, simple objects form the basis for more complex objects, and so on. In deep neural networks we aim to learn these many layers of composable features.

Traditional statistical models do very well on structured data, i.e. tabular data, but have notoriously struggled with unstructured data like images, audio, and natural language. Neural networks that contain many layers of neurons embody the research that is popularly called Deep Learning. The key insight and property of deep neural networks that make them suitable for modeling unstructured data is that complex data, like images, generally have many layers of unique features that are composed to produce the data. As a classic example: images have edges which form the basis for textures, textures form the basis for simple objects, simple objects form the basis for more complex objects, and so on. In deep neural networks we aim to learn these many layers of composable features.

![image](https://user-images.githubusercontent.com/5803001/43685359-4a84c7d4-98e4-11e8-8bce-7ef4cd2aa686.png)

## NLP | 自然语言处理

## Computer Vision | 计算机视觉

# Terminology | 通用概念

## Function | 函数

💡 Sigmod $\sigma$ 💡

神经网络中的激活函数，其作用就是引入非线性。具体的非线性形式，则有多种选择。sigmoid 的优点在于输出范围有限，所以数据在传递的过程中不容易发散。当然也有相应的缺点，就是饱和的时候梯度太小。sigmoid 还有一个优点是输出范围为 (0, 1)，所以可以用作输出层，输出表示概率。Sigmoid 函数是一个在生物学中常见的 S 型的函数，也称为 S 形生长曲线。Sigmoid 函数由下列公式定义，其导数可以节约计算时间:

$$
S(x) = \frac{1}{1+ e^{-x}} \\
S'(x)=S(x)[1-S(x)]
$$

Geoff Hinton covered exactly this topic in his coursera course on neural nets. The problem with sigmoids is that as you reach saturation (values get close to 1 or 0), the gradients vanish. This is detrimental to optimization speed. Softmax doesn't have this problem, and in fact if you combine softmax with a cross entropy error function the gradients are just (z-y), as they would be for a linear output with least squares error.

```py
# sigmoid function
def sigmoid(x, deriv=False):
    if(deriv==True):
        return x*(1-x)
    return 1/(1+np.exp(-x))
```

## Model | 模型

## Optimization | 优化

## Networks | 网络

Gradient ∇ (微分算符)：梯度

梯度即是某个函数的偏导数，其允许输入多个向量然后输出单个值，某个典型的函数即是神经网络中的损失函数。梯度会显示出随着变量输入的增加输出值增加的方向，换言之，如果我们要降低损失值则反梯度逆向前行即可。

梯度下降法 Gradient Descent 是一种常用的一阶(first-order)优化方法，是求解无约束优化问题最简单、最经典的方法之一。考虑无约束优化问题$min_xf(x)$，其中$f(x)$为连续可微函数。如果能构造出一个序列$x^0,x^1,...,x^t$满足：

$$
f(x^{t+1}) < f(x^t),t=0,1,2...
$$

则不断执行该过程即可以收敛到局部极小点。而根据泰勒展示我们可以知道:

$$
f(x+\Delta x) \simeq f(x) + \Delta x^T \nabla f(x)
$$

于是，如果要满足 $f(x+\Delta x) < f(x)$，可以选择:

$$
\Delta x = -{step} \nabla f(x)
$$

其中$step$是一个小常数，表示步长。以求解目标函数最小化为例，梯度下降算法可能存在一下几种情况：

- 当目标函数为凸函数时，局部极小点就对应着函数全局最小值时，这种方法可以快速的找到最优解；
- 当目标函数存在多个局部最小值时，可能会陷入局部最优解。因此需要从多个随机的起点开始解的搜索。
- 当目标函数不存在最小值点，则可能陷入无限循环。因此，有必要设置最大迭代次数。

# Back Propagation：反向传播

简称为 Back prop，即将前向传播输入值计算得出的误差反向传递到输入值中，经常用于微积分中的链式调用。

# Rectified Linear Units or ReLU

Sigmoid 函数的输出间隔为`[0,1]`，而 ReLU 的输出范围为`[0,infinity]`，换言之 Sigmoid 更合适 Logistic 回归而 ReLU 更适合于表示正数。深度学习中 ReLU 并不会受制于所谓的梯度消失问题(Vanishing Gradient Problem)。

# Tanh

Tanh 函数有助于将你的网络权重控制在`[-1,1]`之间，而且从上图中可以看出，越靠近 0 的地方梯度值越大，并且梯度的范围位于`[0,1]`之间，和 Sigmoid 函数的范围一致，这一点也能有助于避免梯度偏差。

# LSTM/GRU

最早见于 Recurrent Neural Networks，不过同样可以用于其他内存单元较少的地方。其主要可以在训练中保持输入的状态，从而避免之前因为 RNN 丢失输入先验上下文而导致的梯度消失问题。

# Softmax

Softmax 函数常用于神经网络的末端以添加分类功能，该函数主要是进行多元逻辑斯蒂回归，也就可以用于多元分类问题。通常会使用交叉熵作为其损失函数。

# L1 & L2 Regularization

正则化项通过对系数添加惩罚项来避免过拟合，正则化项也能够指明模型复杂度。L1 与 L2 的区别在于 L1 能够保证模型的稀疏性。引入正则化项能够保证模型的泛化能力并且避免在训练数据中过拟合。

# Drop out

Drop out 同样可以避免过拟合，并且能以近似指数的时间来合并多个不同的神经网络结构。该方法会随机地在每一层中选择一些显性层与隐层，在我们的实践中通常会由固定比例的层 Drop out 决定。

# Batch Normalization

在深度学习中，如果有太多的层次会导致所谓的 Internal Covariate Shift，也就是训练过程中因为网络参数的变化导致网络激活分布的变化。如果我们能减少这种变量迁移，我们能够更快地训练网络。Batch Normalization 则通过将每个处理块进行正则化处理来解决这个问题。

# Objective Functions

也就是损失函数或者 Optimization Score Function，某个深度学习网络的目标即是最小化该函数值从而提升网络的准确度。

# F1/F Score

用于衡量某个模型的准确度的标准:

```
F1 = 2 * (Precision * Recall) / (Precision + Recall)
Precision = True Positives / (True Positives + False Positives)
Recall = True Positives / (True Positives + False Negatives)
```

# Cross Entropy

用于计算预测标签值与真实标签值之间的差距，基本的定义如下:

# Links

- https://mp.weixin.qq.com/s/TAj6zrxEpQjp0BcwcaEWdQ
