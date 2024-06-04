# TensorFlow CheatSheet | TensorFlow 基础概念与实践清单

TensorFlow 是一个使用数据流图进行数值计算的开放源代码软件库。图中的节点代表数学运算，而图中的边则代表在这些节点之间传递的多维数组（张量）。借助这种灵活的架构，您可以通过一个 API 将计算工作部署到桌面设备、服务器或移动设备中的一个或多个 CPU 或 GPU。TensorFlow 最初是由 Google Brain 团队（隶属于 Google 机器智能研究部门）中的研究人员和工程师开发的，旨在用于进行机器学习和深度神经网络研究。但该系统具有很好的通用性，还可以应用于众多其他领域。

![](https://ww1.sinaimg.cn/large/007rAy9hgy1g05814b4nwj30u00gngvs.jpg)

TensorFlow 是用于表示某种类型的计算抽象（称为计算图）的框架。在使用 TensorFlow 库时，我们首先需要构建计算图，然后初始化 Session，最后填充数据，并且获取结果。

计算图本质上是有向图，也是用于捕获有关如何计算的指令的全局数据结构。

# 基础概念

```py
import tensorflow as tf

# 每次我们调用 tf.constant 时，都会在计算图中创建一个新的节点
two_node = tf.constant(2)
print two_node

# Tensor("Const:0", shape=(), dtype=int32)
```

会话的作用是处理内存分配和优化，使我们能够实际执行由计算图指定的计算。你可以将计算图想象为我们想要执行的计算的模版：它列出了所有步骤。为了使用计算图，我们需要启动一个会话，它使我们能够实际地完成任务；例如，遍历模版的所有节点来分配一堆用于存储计算输出的存储器。

会话包含一个指向全局图的指针，该指针通过指向所有节点的指针不断更新。这意味着在创建节点之前还是之后创建会话都无所谓。创建会话对象后，可以使用 sess.run(node) 返回节点的值，并且 TensorFlow 将执行确定该值所需的所有计算。

```py
two_node = tf.constant(2)
three_node = tf.constant(3)
sum_node = two_node + three_node
sess = tf.Session()
print(sess.run([two_node, sum_node]))

# [2, 5]
```

如果我们需要在计算图中动态地传入数据，则可以使用占位符和 feed_dict，占位符是一种用于接受外部输入的节点:

```py
# 如果不传入占位符值则会抛出异常
input_placeholder = tf.placeholder(tf.int32)
sess = tf.Session()
print sess.run(input_placeholder, feed_dict={input_placeholder: 2})
```

TensorFlow 会自动地帮我们构建计算路径，当我们在依赖于图中其他节点的节点上调用 sess.run() 时，我们也需要计算那些节点的值。如果这些节点具有依赖关系，那么我们需要计算这些值（依此类推……），直到达到计算图的顶端，即节点没有父节点时。TensorFlow 仅通过必需的节点自动进行计算这一事实是该框架的一个巨大优势。如果计算图非常大并且有许多不必要的节点，那么它可以节省大量调用的运行时间。它允许我们构建大型的多用途计算图，这些计算图使用单个共享的核心节点集合，并根据所采取的不同计算路径去做不同的事情。对于几乎所有应用而言，根据所采取的计算路径考虑 sess.run() 的调用是很重要的。

tf.constant 与 tf.placeholder 都是所谓的无祖先(no-ancestor node)节点，我们还需要变量，其值会随着模型的训练而不断变化。需要使用 tf.get_variable(name，shape) 来创建变量，如果要创建一个标量，就需要使用形状为 [] 的空列表。

```py
count_variable = tf.get_variable("count", [])
sess = tf.Session()
print sess.run(count_variable)

'''
Traceback (most recent call last):
...
tensorflow.python.framework.errors_impl.FailedPreconditionError: Attempting to use uninitialized value count
	 [[Node: _retval_count_0_0 = _Retval[T=DT_FLOAT, index=0, _device="/job:localhost/replica:0/task:0/device:CPU:0"](count)]]
'''
```

当我们操作一个尚未赋值的变量时，其会抛出异常；此时我们需要理由 `tf.assign()` 或者初始化函数来初始化变量:

```py
count_variable = tf.get_variable("count", [])
zero_node = tf.constant(0.)
assign_node = tf.assign(count_variable, zero_node)
sess = tf.Session()
sess.run(assign_node)
print(sess.run(count_variable))
```

另一种则是利用全局的初始化函数:

```py
const_init_node = tf.constant_initializer(0.)
count_variable = tf.get_variable("count", [], initializer=const_init_node)
init = tf.global_variables_initializer()
sess = tf.Session()
sess.run(init)
print(sess.run(count_variable))
```

最后，我们需要为计算图添加优化器(Optimizer)模块，以让模型能够真正地学习。在深度学习中，典型的内循环训练如下：

- 获取输入和 true_output

- 根据输入和参数计算推测值

- 根据推测与 true_output 之间的差异计算损失

- 根据损失的梯度更新参数

这里以简单的线性回归问题为例，描述如何构建 TensorFlow 模型:

```py
import tensorflow as tf

### build the graph
## first set up the parameters
m = tf.get_variable("m", [], initializer=tf.constant_initializer(0.))
b = tf.get_variable("b", [], initializer=tf.constant_initializer(0.))
init = tf.global_variables_initializer()

## then set up the computations
input_placeholder = tf.placeholder(tf.float32)
output_placeholder = tf.placeholder(tf.float32)

x = input_placeholder
y = output_placeholder
y_guess = m * x + b

loss = tf.square(y - y_guess)

## finally, set up the optimizer and minimization node
optimizer = tf.train.GradientDescentOptimizer(1e-3)
train_op = optimizer.minimize(loss)

### start the session
sess = tf.Session()
sess.run(init)

### perform the training loop
import random

## set up problem
true_m = random.random()
true_b = random.random()

for update_i in range(100000):
  ## (1) get the input and output
  input_data = random.random()
  output_data = true_m * input_data + true_b

  ## (2), (3), and (4) all take place within a single call to sess.run()!
  _loss, _ = sess.run([loss, train_op], feed_dict={input_placeholder: input_data, output_placeholder: output_data})
  print update_i, _loss

### finally, print out the values we learned for our two variables
print "True parameters:     m=%.4f, b=%.4f" % (true_m, true_b)
print "Learned parameters:  m=%.4f, b=%.4f" % tuple(sess.run([m, b]))
```

`optimizer = tf.train.GradientDescentOptimizer(1e-3)` 不会向计算图中添加节点，它只是创建一个包含有用的帮助函数的 Python 对象。而 `train_op = optimizer.minimize(loss)` 将一个节点添加到图中，并将一个指针存储在变量 train_op 中。train_op 节点没有输出，但是有一个十分复杂的副作用：train_op 回溯输入和损失的计算路径，寻找变量节点。对于它找到的每个变量节点，计算该变量对于损失的梯度。然后计算该变量的新值：当前值减去梯度乘以学习率的积。最后，它执行赋值操作更新变量的值。

因此基本上，当我们调用 sess.run(train_op) 时，它对我们的所有变量做了一个梯度下降的步骤。当然，我们也需要使用 feed_dict 填充输入和输出占位符，并且我们还希望打印损失的值，因为这样方便调试。tf.Print 实际上是一种具有输出和副作用的 Tensorflow 节点，它有两个必需参数：要复制的节点和要打印的内容列表。要复制的节点可以是图中的任何节点；tf.Print 是一个与要复制的节点相关的恒等操作，意味着输出的是输入的副本。但是，它的副作用是打印出打印列表里的所有当前值。

```py
two_node = tf.constant(2)
three_node = tf.constant(3)
sum_node = two_node + three_node
print_sum_node = tf.Print(sum_node, [two_node, three_node])
sess = tf.Session()
print(sess.run(print_sum_node))

# [2][3]
# 5
```

```py
# 数据获取

# 数据处理与划分

# 模型/神经网络构建

# 损失函数

# 变量初始化

# 模型训练

# 模型预测

# 模型导出
```

# 损失函数

## 交叉熵

交叉熵也可以用作损失函数值，其公式定义如下，其中 $q(x)$ 为模型的预估，$p(x)$ 为机器学习中样本的 label:

$$
H(p,q) = -\sum_xp(x)logq(x)
$$

```py
import tensorflow as tf
from random import randint

dims = 8
pos  = randint(0, dims - 1)

logits = tf.random_uniform([dims], maxval=3, dtype=tf.float32)
labels = tf.one_hot(pos, dims)

res1 = tf.nn.softmax_cross_entropy_with_logits(       logits=logits, labels=labels)
res2 = tf.nn.sparse_softmax_cross_entropy_with_logits(logits=logits, labels=tf.constant(pos))

with tf.Session() as sess:
    a, b = sess.run([res1, res2])
    print a, b
    print a == b
```

# 辅助函数

tf.argmax 返回的是 vector 中的最大值的索引号，如果 vector 是一个向量，那就返回一个值，如果是一个矩阵，那就返回一个向量，这个向量的每一个维度都是相对应矩阵行的最大值元素的索引号。

```py
import tensorflow as tf
import numpy as np

A = [[1,3,4,5,6]]
B = [[1,3,4], [2,4,1]]

with tf.Session() as sess:
    print(sess.run(tf.argmax(A, 1)))
    print(sess.run(tf.argmax(B, 1)))
```

# Links

- https://www.jiqizhixin.com/articles/2018-07-02-6
