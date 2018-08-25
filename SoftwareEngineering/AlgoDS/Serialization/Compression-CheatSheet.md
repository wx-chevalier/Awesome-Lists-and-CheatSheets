# Compression CheatSheet | 压缩算法资料索引

RFC 1952 是 GZIP file format specification version 4.3。该规范主要定义了 GZip 压缩的在数据格式方面的规范，以方便不同的操作系统、CPU、文件系统等之间进行文件传输交换。GZIP 的文件格式在设计上其实是可以允许一个文件里有多个压缩数据集（compressed data sets）—— GZIP 压缩后的片段拼接而成的。

每个压缩数据集都是下面的结构：

| ID1 | ID2 | CM | FLG | MTIME（4字节） | XFL | OS | ---> more

| 与 | 之间是 1 byte，都是大端字节（Big Edian）
其中 ID1 和 ID2 分别是 0x1f 和 0x8b，用来标识文件格式是 gzip 
CM 标识 加密算法，目前 0-7是保留字，8 指的是 deflate 算法
FLG 从低地址到高地址分别是 FTEXT、FHCRC、FEXTRA、FNAME、FCOMMENT、reserved、 reserved、reserved，这里每个 bit 被设置了之后有什么意义感兴趣的话可以详细参考 RFC 1952。比较有意思的是 FEXTRA，如果它被设置了表示存在额外的拓展字段。拓展字段的结构如下：
| SI1 | SI2 | LEN | ... LEN bytes of subfield data ... |
SI1、SI2 是对子域的 ID，由 ASCII 码组成。如果你需要使用的话，可以向他的维护者 Jean-Loup Gailly <gzip@prep.ai.mit.edu> 发邮件申请。目前 Apollo file 就有自己的专属 ID
MTIME 指的是源文件最近一次修改时间，存的是 Unix 时间戳
XFL 是给压缩算法传的一些参数，用来标识如何解压。defalte 算法中 2 表示使用压缩率最高的算法，4 表示使用压缩速度最快的算法
OS 标识压缩程序运行的文件系统，以处理 EOF 等的问题
more 后面是根据 FLG 的开启情况决定的，可能会有 循环冗余校验码、源文件长度、附加信息等多种其他信息


# Deflate

GZIP 的核心是 Deflate，在 RFC 1951 中被标准化，并且在当时作为 LZW 的替代品有了非常广泛的使用。

Deflate 是一个同时使用 LZ77 与 Huffman Coding 的算法，这里简单介绍下这两种算法的大致思路：

LZ77

LZ77 的核心思路是如果一个串中有两个重复的串，那么只需要知道第一个串的内容和后面串相对于第一个串起始位置的距离 + 串的长度。

比如： ABCDEFGABCDEFH → ABCDEFG(7,6)H。7 指的是往前第 7 个数开始，6 指的是重复串的长度，ABCDEFG(7,6)H 完全可以表示前面的串，并且是没有二义性的。

LZ77 用滑动窗口（sliding-window compression）来实现这个算法。具体思路是扫描头从串的头部开始扫描串，在扫描头的前面有一个长度为 N 的滑动窗口。如果发现扫描头处的串和窗口里的 最长匹配串 是相同的，则用（两个串之间的距离，串的长度）来代替后一个重复的串，同时还需要添加一个表示是真实串还是替换后的“串”的字节在前面以方便解压（此串需要在 真实串和替换“串” 之前都有存在）。

解压：GZIP 的压缩因为要在窗口里寻找重复串相对来说效率是比较低的（LZ77 还是通过 Hash 等系列方法提高了很多），那解压又是怎么个情况呢？观察压缩后的整个串，每个小串前都有一个标识要标记是原始串还是替换“串”，通过这个标识就能以 O（1）的复杂度直接读完并且替换完替换“串”，整体上效率是非常可观的。

Huffman Coding

Huffman Coding 是大学课本中一般都会提到的算法。核心思路是通过构造 Huffman Tree 的方式给字符重新编码（核心是避免一个叶子的路径是另外一个叶子路径的前缀），以保证出现频路越高的字符占用的字节越少。
