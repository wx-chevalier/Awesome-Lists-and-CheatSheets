[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wxyyxc1992/Awesome-Links)

# 树结构与算法资料索引

* [哈夫曼树](http://blog.csdn.net/shuangde800/article/details/7341289)

* [数据结构和算法系列 16 哈夫曼树](http://www.cnblogs.com/mcgrady/p/3329825.html)

* [2017-Everything you need to know about tree data structures](https://parg.co/U6d): This post is to help you better understand the Tree Data Structure and to clarify any confusion you may have about it.

# 哈夫曼

当树中的节点被赋予一个表示某种意义的数值，我们称之为该节点的权。从树的根节点到任意节点的路径长度(经过的边数)与该节点上权值的乘积称为该节点的带权路径长度。树中所有叶节点的带权路径长度之和称为该树的带权路径长度(WPL)。当带权路径长度最小的二叉树被称为哈夫曼树，也成为最优二叉树。

哈夫曼树在构造时每次从备选节点中挑出两个权值最小的节点进行构造，每次构造完成后会生成新的节点，将构造的节点从备选节点中删除并将新产生的节点加入到备选节点中。新产生的节点权值为参与构造的两个节点权值之和。举例如下：

- [](https://images2015.cnblogs.com/blog/872539/201611/872539-20161104194812346-1641453195.png)

- 备选节点为a,b,c,d，权值分别为7,5,2,4

- 选出c和d进行构造(权值最小),生成新节点为e(权值为6)，备选节点变为7,5,6

- 选出b和e进行构造，生成新节点f(权值为11),备选节点为7,11

- 将最后的7和11节点进行构造，最后生成如图所示的哈夫曼树

## 哈夫曼树的应用

在处理字符串序列时，如果对每个字符串采用相同的二进制位来表示，则称这种编码方式为定长编码。若允许对不同的字符采用不等长的二进制位进行表示，那么这种方式称为可变长编码。可变长编码其特点是对使用频率高的字符采用短编码，而对使用频率低的字符则采用长编码的方式。这样我们就可以减少数据的存储空间，从而起到压缩数据的效果。而通过哈夫曼树形成的哈夫曼编码是一种的有效的数据压缩编码。

