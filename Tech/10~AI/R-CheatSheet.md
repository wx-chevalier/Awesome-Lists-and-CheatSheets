# R CheatSheet

R 语言是基于 S 语言的一种开源实现。S 语言是贝尔实验室最早开发的一种用于统计的工具，后来成为商业的 S-PLUS 软件，是一种与 SAS 和 SPSS 齐名的统计软件。R 语言的一个重要的优势就是 R 的生态，有大量的高质量的第三方的统计和算法相关的包。

```sh
# 查看帮助文档
$ help(sd)
# 查看函数示例
$ example(sd)
```

写好的 R 文件，可以通过 source("filename.R")的形式装载进来。可以通过 save 函数将 R 的内存数据保存到一个 Rdata 文件中。下次再通过 load()函数读取出来。

```r
save(gun_data,file="gun_data.Rdata")
```

可以从 CRAN 上安装扩展包：

```r
# 安装扩展包
install.packages("fBasics")
# 使用扩展包
library(timeDate)
```

# 文件处理

既然要处理数据，肯定要先从数据源读取数据。我们选取最简单的方式，从 csv 文件中读取。假设我们有这样一个 csv 文件：

```csv
times,total, copy
1,122.18138504,48.200
```

我们使用 read.csv 函数将其读到 gun

```r
gun_data <- read.csv("gun-1128-2.csv",header=T,col.names=c("times","total","copy"))
```

# 统计

## 均值

```r
> mean(gun_data3[[2]])
[1] 103.1747
> mean(gun_data4[[2]])
[1] 113.3303
```

## 中位数

均值的问题在于，如果异常值比较大，会把均值拉高或拉低。而中位数是排序后处于中间的数，不受异常值的影响。
R 语言中用 median 函数求中位数：

```r
> median(gun_data3[[2]])
[1] 101.651
```

## 五数

所谓五数，就是最小值，25%分位值，中位数，75%分位值，最大值。
这五个数可以通过 fivenum()函数一次性求出来；连同均值，summary 函数能一次将 6 个数都求出来。

```r
> fivenum(gun_data3[["total"]])
[1]  98.92649 100.48752 101.65097 105.94518 116.74337

> summary(gun_data3[,"total"])
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
  98.93  100.50  101.70  103.20  105.80  116.70
```

## 方差

方差是各样本值与均值的差值的平方的和，反映了数据的离散程度。

> var(gun_data3[,"total"])

- [1] 12.70904

## 标准差

方差的平方根是标准差。R 语言用 sd()函数求标准差

> sd(gun_data3[,"total"])

- [1] 3.564974

## 离差

离差是 R 中提供的一个特殊功能，它是相对于中位数的偏差的绝对值和：

mad(x) = 1/qnorm(3/4) \* median(abs(x-median(x)))
离差用 mad()函数计算。

偏度
如果结果不符合正态分布，我们希望知道是向左偏还是向右偏，这个值用偏度 skewness 来表示。R 中用 skewness()函数来计算。如果值>0 为右偏，反之为左偏。

求偏度的函数，首先要通过 install.packages 来下载 fBasics 库，然后引入 timeDate 库：

> library(timeDate)
> skewness(gun_data3[,2])

- [1] 1.109821
  > attr(,"method")
- [1] "moment"
  > skewness(gun_data4[,2])
- [1] 2.40715
  > attr(,"method")
- [1] "moment"
  > 从中可以看以，这两组数据都向右偏。gun_data4 偏得更厉害。

峰度
峰度是判断这个分布是比正态分布的图更尖还是更平。
R 中用 kurtosis()函数来计算

> kurtosis(gun_data3[,2])

- [1] 0.7986081
  > attr(,"method")
- [1] "excess"
  > kurtosis(gun_data4[,2])
- [1] 7.060265
  > attr(,"method")
- [1] "excess"
  > 上面的两个分布都>0，说明比正态分布都要尖。
