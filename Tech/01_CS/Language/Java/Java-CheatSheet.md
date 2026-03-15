# Java CheatSheet | Java 语法速览与实践清单

当我们谈起 Java 的时候，往往是将其作为一门编程语言来讨论；然而编程语言的特性只是 Java 架构的某部分，保障其平台独立性的一系列底层架构也是 Java 不可分割的组成。宏观来看，我们认为 Java 主要包含以下四个部分：Java 编程语言、Java 类文件格式、Java API 以及 JVM。当我们在进行 Java 开发时，我们使用 Java 编程语言来编写代码，然后将其编译为 Java 类文件，最终在 JVM 中执行这些类文件；目前我们也可以使用 Gradle、Kotlin 等其他优秀的语言来编写 Java 应用程序。而 JVM 与 Java 平台的核心库就构成了我们所熟知的 Java Runtime Environment(JRE)：

在这里，我们首先对于 Java 的常用语法有所了解，可以参考当前目录下的 [java-snippets](https://parg.co/QNJ)。

# Syntax | 语法基础

## 条件选择

## 循环

```java
do{
    System.out.println("Countis:"+count);
    count++;
}while(count<11);
```

# 数据结构

如果需要判断某个对象的类型，可以通过如下方式：

```java
a.getClass().getName()
boolean b = a instanceof String
```

## 数值类型

### 创建与转换

```java
try {
    int result = Integer.parseInt(str);
} catch (NumberFormatException e) {
    System.out.println("notvalid");
}
```

## String | 字符串

```java
// 字符串比较
booleanresult=str1.equals(str2);
booleanresult=str1.equalsIgnoreCase(str2);
```

### 模板字符串

```java
for(inti=0;i<str1.length();i++){
    charaChar=str1.charAt(i);
}
```

### 字符串操作

```java
// 搜索与检索
intresult=str1.indexOf(str2);
intresult=str1.indexOf(str2,5);
Stringindex=str1.substring(14);

// 大小写转化
StringstrUpper=str1.toUpperCase();
StringstrLower=str1.toLowerCase();

// 首尾空格移除
Stringstr1="asdfsdf";
str1.trim();//asdfsdf
// 移除全部空格
str1.replace("","");

// 字符串反转
Stringstr1="whateverstringsomething";
StringBufferstr1buff=newStringBuffer(str1);
Stringstr1rev=str1buff.reverse().toString();

// 字符串转化为数组
Stringstr="tim,kerry,timmy,camden";
String[]results=str.split(",");
```

### Regex | 正则表达式

```java
Stringpattern="\\sa(\\w)*t(\\w)*";//contains"at"
PatternregPat=Pattern.compile(pattern);
// 多行模式
PatternregPat=Pattern.compile(pattern,Pattern.MULTILINE);
Stringtext="wordssomethingatatteafdgdatdsfhey";
Matchermatcher=regPat.matcher(text);
while(matcher.find()){
Stringmatched=matcher.group();
System.out.println(matched);
}
```

## 时间与日期类型

```
DatetodaysDate=newDate();//todaysdate
SimpleDateFormatformatter=newSimpleDateFormat("EEE,ddMMMyyyyHH:mm:ss");//dateformat
StringformattedDate=formatter.format(todaysDate);
System.out.println(formattedDate);
```

Java 8 为我们提供了 LocalDate 等类型：

```java
longstartTime=System.currentTimeMillis();
//timesfliesby..
longfinishTime=System.currentTimeMillis();
longtimeElapsed=startTime-finishTime;
System.out.println(timeElapsed);
```

# Collection | 集合类型

## 数组

### 构建与检索

```java
// 数组复制
int[] myArray = new int[10];

int[] tmp = new int[myArray.length+10];
System.arraycopy(myArray,0,tmp,0,myArray.length);
myArray=tmp;

// 将 List 转化为数组
String[] stockArr = new String[stockList.size()];
stockArr = stockList.toArray(stockArr);
// HashMap 转化为数组
Object[] objects = hashmap.entrySet().toArray();

// 将 Stream 转化为数组
Stream<String> stringStream = Stream.of("a", "b", "c");

String[] stringArray = stringStream.toArray(size -> new String[size]);
String[] stringArray = stringStream.toArray(String[]::new);

Arrays.stream(stringArray).forEach(System.out::println);
```

### 排序

```java
int[]nums={1,4,7,324,0,-4};
Arrays.sort(nums);
```

## List

### 创建增删

### 检索排序

```java
List<String>unsortList = newArrayList<String>();
Collections.sort(unsortList);

// 二分搜索
int[]nums = new int[]{7,5,1,3,6,8,9,2};
Arrays.sort(nums);
int index = Arrays.binarySearch(nums,6);
System.out.println("6 isatindex:" + index);
```

## Map

```java
HashMap map = new HashMap();
map.put(key1,obj1);

map.containsValue(obj);
```

```java
// 遍历集合
for(Iteratorit=map.entrySet().iterator();it.hasNext();){
    Map.Entryentry=(Map.Entry)it.next();
    Objectkey=entry.getKey();
    Objectvalue=entry.getValue();
}
```

#### 比较 Double:

```
Doublea=4.5;
    Doubleb=4.5;

    booleanresult=a.equals(b);

    if(result)System.out.println("equal");
```

####rounding:

```
doubledoubleVal=43.234234200000000234040324;
    floatfloatVal=2.98f;

    longlongResult=Math.round(doubleVal);
    intintResult=Math.round(floatVal);

    System.out.println(longResult+"and"+intResult);//43and3
```

#### 格式化数字:

```
doublevalue=2343.8798;
    NumberFormatnumberFormatter;
    StringformattedValue;
    numberFormatter=NumberFormat.getNumberInstance();
    formattedValue=numberFormatter.format(value);
    System.out.format("%s%n",formattedValue);//2.343,88
```

#### 格式化货币:

```
doublecurrency=234546457.99;
    NumberFormatcurrencyFormatter;
    StringformattedCurrency;

    currencyFormatter=NumberFormat.getCurrencyInstance();

    formattedCurrency=currencyFormatter.format(currency);

    System.out.format("%s%n",formattedCurrency);//$234.546.457,99
```

#### 二进制、八进制、十六进制转换:

```
intval=25;
StringbinaryStr=Integer.toBinaryString(val);
StringoctalStr=Integer.toOctalString(val);
StringhexStr=Integer.toHexString(val);
```

#### 随机数生成:

```
doublern=Math.random();
    intrint=(int)(Math.random()*10);//randomintbetween0-10

    System.out.println(rn);
    System.out.println(rint);
```

#### 计算三角函数:

```
doublecos=Math.cos(45);
    doublesin=Math.sin(45);
    doubletan=Math.tan(45);
```

#### 读取二进制数据:

InputStreamis=newFileInputStream(fileName);

```
intoffset=0;
intbytesRead=is.read(bytes,ofset,bytes.length-offset);
```

#### 文件随机访问:

```
Filefile=newFile(something.bin);
RandomAccessFileraf=newRandomAccessFile(file,"rw");
raf.seek(file.length());
```

#### 读取 Jar/zip/rar 文件:

```
ZipFilefile=newZipFile(filename);
Enumerationentries=file.entries();
while(entries.hasMoreElements()){

    ZipEntryentry=(ZipEntry)entries.nextElement();
    if(entry.isDirectory()){
        //dosomething
    }
    else{
        //dosomething
    }
}
file.close();
```

## 文件与目录

#### 创建文件:

```
Filef=newFile("textFile.txt");
booleanresult=f.createNewFile();
```

#### 文件重命名:

Filef=newFile("textFile.txt");

```
Filenewf=newFile("newTextFile.txt");
booleanresult=f.renameto(newf);
```

#### 删除文件:

```
Filef=newFile("somefile.txt");
f.delete();
```

#### 改变文件属性:

```
Filef=newFile("somefile.txt");
f.setReadOnly();//makingthefilereadonly
f.setLastModified(desiredtime);
```

#### 获取文件大小:

```
Filef=newFile("somefile.txt");
longlength=file.length();
```

#### 判断文件是否存在:

```
Filef=newFile("somefile.txt");
booleanstatus=f.exists();
```

#### 移动文件:

```
Filef=newFile("somefile.txt");
Filedir=newFile("directoryName");
booleansuccess=f.renameTo(newFile(dir,file.getName()));
```

#### 获取绝对路径:

```
Filef=newFile("somefile.txt");
FileabsPath=f.getAbsoluteFile();
```

#### 判断是文件还是目录:

```
Filef=newFile("somefile.txt");
booleanisDirectory=f.isDirectory();
System.out.println(isDirectory);//false
```

```java
// 列举目录下文件
Filedirectory=newFile("users/ege");
String[]result=directory.list();

// 创建目录
booleanresult=newFile("users/ege").mkdir();
```

## 网络客户端

#### 服务器连接:

```
StringserverName="www.egek.us";
Socketsocket=newSocket(serverName,80);
System.out.println(socket);
```

#### 网络异常处理:

```java
try{
        Socketsock=newSocket(server_name,tcp_port);
        System.out.println("Connectedto"+server_name);
    sock.close();

}catch(UnknownHostExceptione){
    System.err.println(server_name+"Unknownhost");
    return;
}catch(NoRouteToHostExceptione){
    System.err.println(server_name+"Unreachable");
    return;
}catch(ConnectExceptione){
    System.err.println(server_name+"connectrefused");
    return;
}catch(java.io.IOExceptione){
    System.err.println(server_name+''+e.getMessage());
    return;
}
```

## 包与文档

#### 创建包:

```
packagecom.ege.example;
```

#### 使用 JavaDoc 注释某个类:

```
javadoc-d\home\html
-sourcepath\home\src
-subpackagesjava.net
```

# 类与对象

## 实例化

### 单例模式

```java
public class Singleton {
　　private static volatile Singleton instance = null;

　　public static Singleton getInstance() {
　　　　if (instance == null) {
　　　　　　　　synchronized (Singleton.class) {
　　　　　　　　　　　　if (instance == null) {
　　　　　　　　　　　　　　　　instance ＝ new Singleton();
　　　　　　　　　　　　}
　　　　　　　　}
　　　　}
　　　　return instance;
　　}
}
```

## Interface

### Functional Interface & Lambda

Java 原本作为纯粹的面向对象的语言，需要对 Lambda 表达式特性进行支持，其实是基于了一种特殊的函数式接口。换言之，`()->{}` 这样的语法本质上还是继承并且实现了一个接口。FI 的定义其实很简单：任何接口，如果只包含 唯一 一个抽象方法，那么它就是一个 FI。为了让编译器帮助我们确保一个接口满足 FI 的要求(也就是说有且仅有一个抽象方法)，Java8 提供了@FunctionalInterface 注解。以 Runnble 为例：

```java
@FunctionalInterface
public interface Runnable {
  public abstract void run();
}
```

常见的内置函数式接口还有如下：

```java
Predicate<String> predicate = (s) -> s.length() > 0;

Comparator<Person> comparator = (p1, p2) -> p1.firstName.compareTo(p2.firstName);
```

闭包一般指存在自由变量的代码块，它与对象类似，都是用来描述一段代码与其环境的关系。在 Java 中，Lambda 表达式就是闭包。Lambda 表达式本身是构造了一个继承自某个函数式接口的子类，所以可以用父类指针指向它。Java 中本质上闭包中是采用的值捕获，即不可以在闭包中使用可变对象。但是它实际上是允许捕获事实上不变量，譬如不可变的 ArrayList，只是指针指向不可变罢了。

Lambda 表达式还可以进一步简化为方法引用(Method References)，一共有四种形式的方法引用：

```java
// 静态方法引用
List<Integer> ints = Arrays.asList(1, 2, 3);
ints.sort(Integer::compare);

// 某个特定对象的实例方法
words.forEach(System.out::println);

// 某个类的实例方法
words.stream().map(word -> word.length()); // lambda
words.stream().map(String::length); // method reference

// 构造函数引用
words.stream().map(word -> {
return new StringBuilder(word);
});
// constructor reference
words.stream().map(StringBuilder::new);
```

## Stream

Java 8 API 添加了一个新的抽象称为流 Stream，可以让你以一种声明的方式处理数据；Stream 使用一种类似用 SQL 语句从数据库查询数据的直观方式来提供一种对 Java 集合运算和表达的高阶抽象。这种风格将要处理的元素集合看作一种流，流在管道中传输，并且可以在管道的节点上进行处理，比如筛选，排序，聚合等。

Stream（流）是一个来自数据源的元素队列并支持聚合操作，元素是特定类型的对象，形成一个队列；Java 中的 Stream 并不会存储元素，而是按需计算。元素流在管道中经过中间操作(intermediate operation)的处理，最后由最终操作(terminal operation)得到前面处理的结果。

```sh
+--------------------+     +------+   +------+   +---+   +-------+
| stream of elements +-----> |filter+-> |sorted+-> |map+-> |collect|
+--------------------+     +------+   +------+   +---+   +-------+
```

最简流程的描述如下：

```java
List<Integer> transactionsIds =
widgets.stream()
     .filter(b -> b.getColor() == RED)
     .sorted((x,y) -> x.getWeight() - y.getWeight())
     .mapToInt(Widget::getWeight)
     .sum();
```

和以前的 Collection 操作不同，Stream 操作还有两个基础的特征：

- Pipelining: 中间操作都会返回流对象本身。这样多个操作可以串联成一个管道，如同流式风格（fluent style）。这样做可以对操作进行优化，比如延迟执行(laziness)和短路( short-circuiting)。
- 内部迭代：以前对集合遍历都是通过 Iterator 或者 For-Each 的方式, 显式的在集合外部进行迭代，这叫做外部迭代。Stream 提供了内部迭代的方式，通过访问者模式(Visitor)实现。

## 流构建

```java
List<String> strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");

// 创建串行流
List<String> filtered = strings.stream().filter(string -> !string.isEmpty()).collect(Collectors.toList());

// 创建并行流，获取空字符串的数量
int count = strings.parallelStream().filter(string -> string.isEmpty()).count();

// 构建空流
Stream<String> streamEmpty = Stream.empty();

// 构建数值流
IntStream intStream = IntStream.range(1, 3); // 1, 2
LongStream longStream = LongStream.rangeClosed(1, 3);
Random random = new Random();
DoubleStream doubleStream = random.doubles(3);

// 构建数组流
Stream<String> streamOfArray = Stream.of("a", "b", "c");
String[] arr = new String[]{"a", "b", "c"};
Stream<String> streamOfArrayFull = Arrays.stream(arr);
Stream<String> streamOfArrayPart = Arrays.stream(arr, 1, 3);

// 构建文件流
Path path = Paths.get("C:\\file.txt");
Stream<String> streamOfStrings = Files.lines(path);
Stream<String> streamWithCharset =
  Files.lines(path, Charset.forName("UTF-8"));
```

## Transform

```java
// map 方法用于映射每个元素到对应的结果
List<Integer> numbers = Arrays.asList(3, 2, 2, 3, 7, 3, 5);

// 获取对应的平方数
List<Integer> squaresList = numbers.stream().map( i -> i*i).distinct().collect(Collectors.toList());

// filter 方法用于通过设置的条件过滤出元素。以下代码片段使用 filter 方法过滤出空字符串
int count = strings.stream().filter(string -> string.isEmpty()).count();

// limit 方法用于获取指定数量的流。以下代码片段使用 limit 方法打印出 10 条数据
Random random = new Random();
random.ints().limit(10).forEach(System.out::println);

// sorted 方法用于对流进行排序
Random random = new Random();
random.ints().limit(10).sorted().forEach(System.out::println);
```

## Collectors | 归约操作

```java
List<String>strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");

List<String> filtered = strings.stream().filter(string -> !string.isEmpty()).collect(Collectors.toList());
System.out.println("筛选列表: " + filtered);

String mergedString = strings.stream().filter(string -> !string.isEmpty()).collect(Collectors.joining(", "));
System.out.println("合并字符串: " + mergedString);
```

```java
// 提取为 Map
IntStream.range(0, alphabet.size())
     .boxed()
     .collect(toMap(alphabet::get, i -> i));
```

# 数据结构

## 数组

```java
// Array 转化为  List
List<Integer> numbers = Arrays.asList(3, 2, 2, 3, 7, 3, 5);

// List 转化为 Array
List<String> stockList = new ArrayList<String>();
...
String[] stockArr = new String[stockList.size()];
stockArr = stockList.toArray(stockArr);
```

# Network | 网络

# Storage | 存储

## 文件读写

Java.io 包几乎包含了所有操作输入、输出需要的类。所有这些流类代表了输入源和输出目标；Java.io 包中的流支持很多种格式，比如：基本类型、对象、本地化字符集等等。一个流可以理解为一个数据的序列。输入流表示从一个源读取数据，输出流表示向一个目标写数据。Java 为 IO 提供了强大的而灵活的支持，使其更广泛地应用到文件传输和网络编程中。

InputStream 是所有字节输入流的祖先，而 OutputStream 是所有字节输出流的祖先；Reader 是所有读取字符串输入流的祖先，而 writer 是所有输出字符串的祖先。字节流是最基本的，所有的 InputStream 和 OutputStream 的子类都是,主要用在处理二进制数据，它是按字节来处理的，但实际中很多的数据是文本，又提出了字符流的概念，它是按虚拟机的 Encode 来处理，也就是要进行字符集的转化。这两个之间通过 InputStreamReader,OutputStreamWriter 来关联，实际上是通过 byte[]和 String 来关联。字节流在操作时本身不会用到缓冲区（内存），是文件本身直接操作的，而字符流在操作时使用了缓冲区，通过缓冲区再操作文件。

![](http://www.runoob.com/wp-content/uploads/2013/12/iostream2xx.png)

控制台读写：

```java
BufferedReaderinStream=newBufferedReader(newInputStreamReader(System.in));
Stringinline="";
while(!(inline.equalsIgnoreCase("quit"))){
System.out.println("prompt>");
inline=inStream.readLine();
}
```

```java
BufferedReaderbr=newBufferedReader(newFileReader(textFile.txt));//forreading
BufferedWriterbw=newBufferedWriter(newFileWriter(textFile.txt));//forwriting
```

## 文件系统

```java
{Thread.currentThread().getContextClassLoader() / SomeClass.class}.
{getResource("").getFile() / getResourceAsStream()}
```

# Links

- https://github.com/in28minutes/java-cheat-sheet
