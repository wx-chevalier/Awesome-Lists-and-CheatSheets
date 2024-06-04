# Python 语法速览与实战清单

Python CheatSheet 是对于 Python 学习/实践过程中的语法与技巧进行盘点，其属于 [Awesome CheatSheet](https://github.com/wx-chevalier/Awesome-CheatSheets/) 系列，致力于提升学习速度与研发效能，即可以将其当做速查手册，也可以作为轻量级的入门学习资料。本文参考了许多优秀的文章与代码示范，统一声明在了 [Python Links](https://github.com/wx-chevalier/Awesome-Lists/blob/master/ProgrammingLanguage/Python/Python-List.md)；如果希望深入了解某方面的内容，可以继续阅读[]()，或者前往 [coding-snippets/python]() 查看使用 Python 解决常见的数据结构与算法、设计模式、业务功能方面的代码实现。

According to its creator, Guido van Rossum, Python is a:“high-level programming language, and its core design philosophy is all about code readability and a syntax which allows programmers to express concepts in a few lines of code.”

建议使用 [pipenv](https://github.com/pypa/pipenv) 作为项目环境管理：

```sh
# 创建 Python 2/3 版本的项目
$ pipenv --two/--three

# 安装项目依赖，会在当前目录下生成 .venv 目录，包含 python 解释器
$ pipenv install
$ pipenv install --dev

# 弹出 Virtual Env 对应的脚本环境
$ pipenv shell

# 执行文件
$ pipenv run python

# 定位项目路径
$ pipenv --where
/Users/kennethreitz/Library/Mobile Documents/com~apple~CloudDocs/repos/kr/pipenv/test

# 定位虚拟环境路径
$ pipenv --venv
/Users/kennethreitz/.local/share/virtualenvs/test-Skyy4vre

# 定位 Python 解释器路径
$ pipenv --py
/Users/kennethreitz/.local/share/virtualenvs/test-Skyy4vre/bin/python
```

如果遇到编码问题，可以设置如下环境变量：

```sh
export LC_ALL=zh_CN.UTF-8
export LANG=zh_CN.UTF-8
```

如果遇到网络问题，可以尝试使用国内的镜像源：

```Pipfile
[[source]]
url = "https://mirrors.ustc.edu.cn/pypi/web/simple"
verify_ssl = true
name = "pypi"
```

在这里，我们首先对于 Python 的常用语法有所了解，可以参考 [python-snippets](./python-snippets.py)。

# 基础语法

Python 是一门高阶、动态类型的多范式编程语言；定义 Python 文件的时候我们往往会先声明文件编码方式

```py
# 指定脚本调用方式
#!/usr/bin/env python
# 配置 utf-8 编码
# -*- coding: utf-8 -*-

# 配置其他编码
# -*- coding: <encoding-name> -*-

# Vim 中还可以使用如下方式
# vim:fileencoding=<encoding-name>

# Python 中的注释方式
# 这是一个注释

'''
这是多行注释，用三个单引号
'''

"""
这是多行注释，用三个双引号
"""
```

人生苦短，请用 Python，大量功能强大的语法糖的同时让很多时候 Python 代码看上去有点像伪代码。譬如我们用 Python 实现的简易的快排相较于 Java 会显得很短小精悍

```py
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) / 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)

print quicksort([3,6,8,10,1,2,1])
# Prints "[1, 1, 2, 3, 6, 8, 10]"
```

## 控制台交互

可以根据 `__name__` 关键字来判断是否是直接使用 python 命令执行某个脚本，还是外部引用；Google 开源的 fire 也是不错的快速将某个类封装为命令行工具的框架：

```py
import fire

class Calculator(object):
  """A simple calculator class."""

  def double(self, number):
    return 2 * number

if __name__ == '__main__':
  fire.Fire(Calculator)

# python calculator.py double 10  # 20
# python calculator.py double --number=15  # 30
```

Python 2 中 print 是表达式，而 Python 3 中 print 是函数；如果希望在 Python 2 中将 print 以函数方式使用，则需要自定义引入

```py
from __future__ import print_function
```

我们也可以使用 pprint 来美化控制台输出内容：

```py
import pprint

stuff = ['spam', 'eggs', 'lumberjack', 'knights', 'ni']
pprint.pprint(stuff)

# 自定义参数
pp = pprint.PrettyPrinter(depth=6)
tup = ('spam', ('eggs', ('lumberjack', ('knights', ('ni', ('dead',('parrot', ('fresh fruit',))))))))
pp.pprint(tup)
```

## 模块

Python 中的模块(Module)即是 Python 源码文件，其可以导出类、函数与全局变量；当我们从某个模块导入变量时，函数名往往就是命名空间(Namespace)。

而 Python 中的包（Package）则是模块的文件夹，往往由 `__init__.py` 指明某个文件夹为包，Package 可以为某个目录下所有的文件设置统一入口

```py
# 目录格式
someDir/
	main.py
	subModules/
		__init__.py
		subA.pys
		subSubModules/
			__init__.py
			subSubA.py

# subA.py
def subAFun():
	print('Hello from subAFun')

def subAFunTwo():
	print('Hello from subAFunTwo')

# subSubA.py
def subSubAFun():
	print('Hello from subSubAFun')

def subSubAFunTwo():
	print('Hello from subSubAFunTwo')

# __init__.py from subDir

# 将 'subAFun()' 与 'subAFunTwo()' 添加到 'subModules' 命名空间
from subA import *

# 假设 'subSubModules' 中的 '__init__.py' 为空
# 将 'subSubAFun()' 与 'subSubAFunTwo()' 添加到 'subModules' 命名空间
from subSubModules.subSubA import *

# 假设 'subSubModules' 中的 '__init__.py' 不为空，包含了 'from .subSubA import *'
# __init__.py，将 'subSubAFun()' 与 'subSubAFunTwo()' 添加到 'subSubModules' 命名空间
from subSubA import *

# 将 'subSubAFun()' 与 'subSubAFunTwo()' 添加到 'subModules' 命名空间
from subSubDir import *

# main.py
import subDir

subDir.subAFun() # Hello from subAFun
subDir.subAFunTwo() # Hello from subAFunTwo
subDir.subSubAFun() # Hello from subSubAFun
subDir.subSubAFunTwo() # Hello from subSubAFunTwo
```

`__init__.py` 中也支持使用 `__all__` 变量来声明所有需要导出的子模块:

```py
import submodule1
import submodule2

__all__ = ['submodule1', 'submodule2']
```

Python 中只能在 Package 中使用相对导入，不能在用户的应用程序中使用相对导入，因为不论是相对导入还是绝对导入，都是相当于当前模块来说的，对于用户的主应用程序，也就是入口文件，模块名总是 `__main__`, 所以用户的应用程序必须使用绝对导入，而 Package 中的导入可以使用相对导入。

```py
# python -m 运行该文件
from .some_module import some_class
from ..some_package import some_function
from . import some_class

import foo.baz # absolute import, always OK
from . import .baz # explicit relative import, Python >= 2.5, Py3
import baz # implicit relative import, OK in Python < 2.5, deprecated in Python >= 2.5, error in Python 3
```

### 动态加载

Python 支持动态地加载模块文件，即从某个文件中手动初始化对象：

```py
def get_factory_from_template(maintype):
    path = os.path.join(BASE_DIR, 'templates', maintype, FACTORY_FILENAME)
    if (python_version_gte(3, 5)):
        # Python 3.5 code in this block
        import importlib.util
        spec = importlib.util.spec_from_file_location(
            "{}.factory".format(maintype), path)
        foo = importlib.util.module_from_spec(spec)
        spec.loader.exec_module(foo)
        return foo
    elif (python_version_gte(3, 0)):
        from importlib.machinery import SourceFileLoader
        foo = SourceFileLoader(
            "{}.factory".format(maintype), path).load_module()
        return foo
    else:
        # Python 2 code in this block
        import imp
        foo = imp.load_source("{}.factory".format(maintype), path)
        return foo
```

### 自定义模块

我们可以通过定义 setup.py 来创建自定义模块:

```py
# pipenv install -e . 来安装本地目录的依赖
from setuptools import setup, find_packages

setup(
    name = "test",
    version = "1.0",
    keywords = ("test", "xxx"),
    description = "eds sdk",
    long_description = "eds sdk for python",
    license = "MIT Licence",

    url = "http://test.com",
    author = "test",
    author_email = "test@gmail.com",

    packages = find_packages(),
    include_package_data = True,
    platforms = "any",
    install_requires = [],

    scripts = [],
    entry_points = {
        'console_scripts': [
            'test = test.help:main'
        ]
    }
)
```

# 表达式与控制流

## 条件选择

Python 中使用 if、elif、els#e 来进行基础的条件选择操作：

```py
if x < 0:
     x = 0
     print('Negative changed to zero')
 elif x == 0:
     print('Zero')
 else:
     print('More')
```

Python 同样支持 ternary conditional operator，并且提供了

```py
a if condition else b

x = [True, True, False]
if any(x):
    print("At least one True")
if all(x):
    print("Not one False")
if any(x) and not all(x):
    print("At least one True and one False")
```

也可以使用 Tuple 来实现类似的效果：

```py
# test 需要返回 True 或者 False
(falseValue, trueValue)[test]

# 更安全的做法是进行强制判断
(falseValue, trueValue)[test == True]

# 或者使用 bool 类型转换函数
(falseValue, trueValue)[bool(<expression>)]
```

## 循环遍历

for-in 可以用来遍历数组与字典：

```py
words = ['cat', 'window', 'defenestrate']

for w in words:
    print(w, len(w))

# 使用数组访问操作符，能够迅速地生成数组的副本
for w in words[:]:
    if len(w) > 6:
        words.insert(0, w)

# words -> ['defenestrate', 'cat', 'window', 'defenestrate']
```

如果我们希望使用数字序列进行遍历，可以使用 Python 内置的 `range` 函数：

```py
a = ['Mary', 'had', 'a', 'little', 'lamb']

for i in range(len(a)):
    print(i, a[i])
```

[tqdm](https://github.com/tqdm/tqdm) 是不错的命令行中的进度指示器：

```py
from tqdm import tqdm
for i in tqdm(range(10000)):
    ...
```

# 基本数据类型

可以使用内建函数进行强制类型转换(Casting )

```py
int(str)
float(str)
str(int)
str(float)
```

isinstance 方法用于判断某个对象是否源自某个类

```py
ex = 10

# 判断是否为 int 类型
isinstance(ex,int)

# isinstance 也支持同时判断多个类型
# 如下代码判断是否为数组
def is_array(var):
    return isinstance(var, (list, tuple))
```

## Number | 数值类型

```py
x = 3
print type(x) # Prints "<type 'int'>"
print x       # Prints "3"
print x + 1   # Addition; prints "4"
print x - 1   # Subtraction; prints "2"
print x * 2   # Multiplication; prints "6"
print x ** 2  # Exponentiation; prints "9"
x += 1
print x  # Prints "4"
x *= 2
print x  # Prints "8"
y = 2.5
print type(y) # Prints "<type 'float'>"
print y, y + 1, y * 2, y ** 2 # Prints "2.5 3.5 5.0 6.25"
```

Python2 中默认使用传统除法，即自动四舍五入；而 Python 3 中默认使用精确除法：

```py
# 传统除法 如果是整数除法则执行地板除，如果是浮点数除法则执行精确除法。
> 1/2
0
> 1.0/2.0
0.5

# 精确除法 除法总是会返回真实的商，不管操作数是整形还是浮点型。

# ‘//’无论是否整除返回的都是 int，而且是去尾整除
>>> 5//2
2

# 向上取整，返回值为 int
> math.ceil()

# 向下取整，返回值为 int
> math.floor()

# 返回值为 int
> round()
```

## 布尔类型

Python 提供了常见的逻辑操作符，不过需要注意的是 Python 中并没有使用 &&、|| 等，而是直接使用了英文单词。

```py
t = True
f = False
print type(t) # Prints "<type 'bool'>"
print t and f # Logical AND; prints "False"
print t or f  # Logical OR; prints "True"
print not t   # Logical NOT; prints "False"
print t != f  # Logical XOR; prints "True"
```

## String | 字符串

Python 2 中支持 Ascii 码的 str() 类型，独立的 unicode() 类型，没有 byte 类型；而 Python 3 中默认的字符串为 utf-8 类型，并且包含了 byte 与 bytearray 两个字节类型：

```py
type("Guido") # string type is str in python2
# <type 'str'>

# 使用 __future__ 中提供的模块来降级使用 Unicode
from __future__ import unicode_literals
type("Guido") # string type become unicode
# <type 'unicode'>
```

Python 字符串支持分片、模板字符串等常见操作

```py
var1 = 'Hello World!'
var2 = "Python Programming"

print "var1[0]: ", var1[0]
print "var2[1:5]: ", var2[1:5]
# var1[0]:  H
# var2[1:5]:  ytho

print "My name is %s and weight is %d kg!" % ('Zara', 21)
# My name is Zara and weight is 21 kg!
```

```py
str[0:4]
len(str)

string.replace("-", " ")
",".join(list)
str.find(",")
str.index(",")   # same, but raises IndexError
str.count(",")
str.split(",")

str.lower()
str.upper()
str.title()

str.lstrip()
str.rstrip()
str.strip()

str.islower()
```

```py
# 移除所有的特殊字符
re.sub('[^A-Za-z0-9]+', '', mystring)
```

如果需要判断是否包含某个子字符串，或者搜索某个字符串的下标

```py
# in 操作符可以判断字符串
if "blah" not in somestring:
    continue

# find 可以搜索下标
s = "This be a string"
if s.find("is") == -1:
    print "No 'is' here!"
else:
    print "Found 'is' in the string."
```

### 模板字符串

```py
import datetime

name = 'Fred'
age = 50
anniversary = datetime.date(1991, 10, 12)

x = a + b
x = '%s, %s!' % (name, age)
x = 'name: %s; age: %d' % (name, age)
x = '{}, {}!'.format(name, age)
x = 'name: {}; age: {}'.format(name, age)

f'My name is {name}, my age next year is {age+1}, my anniversary is {anniversary:%A, %B %d, %Y}.'
# 'My name is Fred, my age next year is 51, my anniversary is Saturday, October 12, 1991.'

f'He said his name is {name!r}.'
# "He said his name is 'Fred'."
```

## Regex | 正则表达式

- Symbols

| Term | Description                                                    |
| ---- | -------------------------------------------------------------- |
| .    | (period) Matches any single character, except for line breaks. |
| \*   | Matches the preceding expression 0 or more times.              |
| +    | Matches the preceding expression 1 or more times.              |
| ?    | Preceding expression is optional (Matches 0 or 1 times).       |
| ^    | Matches the beginning of the string.                           |
| \$   | Matches the end of the string.                                 |

- Character groups

| Term   | Description                                                                                                               |
| ------ | ------------------------------------------------------------------------------------------------------------------------- |
| \d     | Matches any single digit character.                                                                                       |
| \w     | Matches any word character (alphanumeric & underscore).                                                                   |
| [XYZ]  | Character Set: Matches any single character from the character within the brackets. You can also do a range such as [A-Z] |
| [XYZ]+ | Matches one or more of any of the characters in the set.                                                                  |
| [^a-z] | Inside a character set, the ^ is used for negation. In this example, match anything that is NOT an uppercase letter.      |

- Flags:
  There are five optional flags. They can be used separately or together and are placed after the closing slash. Example: /[A-Z]/g I’ll only be introducing 2 here.

| Term | Description             |
| ---- | ----------------------- |
| g    | Global search           |
| i    | case insensitive search |

- Advanced

| Term   | Description                                                               |
| ------ | ------------------------------------------------------------------------- |
| (x)    | Capturing Parenthesis: Matches x and remembers it so we can use it later. |
| (?:x)  | Non-capturing Parenthesis: Matches x and does not remembers it.           |
| x(?=y) | Lookahead: Matches x only if it is followed by y.                         |

```py
import re

# 判断是否匹配
re.match(r'^[aeiou]', str)

# 以第二个参数指定的字符替换原字符串中内容
re.sub(r'^[aeiou]', '?', str)
re.sub(r'(xyz)', r'\1', str)

# 编译生成独立的正则表达式对象
expr = re.compile(r'^...$')
expr.match(...)
expr.sub(...)
```

如果我们需要提取出正则表达式中的匹配组，则需要理由正则表达式的中括号与 group 方法:

```py
title_search = re.search('<title>(.*)</title>', html, re.IGNORECASE)

if title_search:
    title = title_search.group(1)
```

下面列举了常见的表达式使用场景

```py
# 检测是否为 HTML 标签
re.search('<[^/>][^>]*>', '<a href="#label">')

# 常见的用户名密码
re.match('^[a-zA-Z0-9-_]{3,16}$', 'Foo') is not None
re.match('^\w|[-_]{3,16}$', 'Foo') is not None

# Email
re.match('^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$', 'hello.world@example.com')

# Url
exp = re.compile(r'''^(https?:\/\/)? # match http or https
                ([\da-z\.-]+)            # match domain
                \.([a-z\.]{2,6})         # match domain
                ([\/\w \.-]*)\/?$        # match api or file
                ''', re.X)
exp.match('www.google.com')

# IP 地址
exp = re.compile(r'''^(?:(?:25[0-5]
                     |2[0-4][0-9]
                     |[1]?[0-9][0-9]?)\.){3}
                     (?:25[0-5]
                     |2[0-4][0-9]
                     |[1]?[0-9][0-9]?)$''', re.X)
exp.match('192.168.1.1')
```

# 集合类型

## List | 列表

### Operation | 创建增删

list 是基础的序列类型：

```py
l = []
l = list()

# 使用字符串的 split 方法，可以将字符串转化为列表
str.split(".")

# 如果需要将数组拼装为字符串，则可以使用 join
list1 = ['1', '2', '3']
str1 = ''.join(list1)

# 如果是数值数组，则需要先进行转换
list1 = [1, 2, 3]
str1 = ''.join(str(e) for e in list1)
```

可以使用 append 与 extend 向数组中插入元素或者进行数组连接

```py
x = [1, 2, 3]

x.append([4, 5]) # [1, 2, 3, [4, 5]]

x.extend([4, 5]) # [1, 2, 3, 4, 5]，注意 extend 返回值为 None
```

可以使用 pop、slices、del、remove 等移除列表中元素：

```py
myList = [10,20,30,40,50]

# 弹出第二个元素
myList.pop(1) # 20
# myList: myList.pop(1)

# 如果不加任何参数，则默认弹出最后一个元素
myList.pop()

# 使用 slices 来删除某个元素
a = [1, 2, 3, 4, 5, 6 ]
index = 3 # Only Positive index
a = a[:index] + a[index+1 :]

# 根据下标删除元素
myList = [10,20,30,40,50]
rmovIndxNo = 3
del myList[rmovIndxNo] # myList: [10, 20, 30, 50]

# 使用 remove 方法，直接根据元素删除
letters = ["a", "b", "c", "d", "e"]
numbers.remove(numbers[1])
print(*letters) # used a * to make it unpack you don't have to
```

### Iteration | 索引遍历

你可以使用基本的 for 循环来遍历数组中的元素，就像下面介个样纸

```py
animals = ['cat', 'dog', 'monkey']
for animal in animals:
    print animal
# Prints "cat", "dog", "monkey", each on its own line.
```

如果你在循环的同时也希望能够获取到当前元素下标，可以使用 enumerate 函数

```py
animals = ['cat', 'dog', 'monkey']
for idx, animal in enumerate(animals):
    print '#%d: %s' % (idx + 1, animal)
# Prints "#1: cat", "#2: dog", "#3: monkey", each on its own line
```

Python 也支持切片(Slices):

```py
nums = range(5)    # range is a built-in function that creates a list of integers
print nums         # Prints "[0, 1, 2, 3, 4]"
print nums[2:4]    # Get a slice from index 2 to 4 (exclusive); prints "[2, 3]"
print nums[2:]     # Get a slice from index 2 to the end; prints "[2, 3, 4]"
print nums[:2]     # Get a slice from the start to index 2 (exclusive); prints "[0, 1]"
print nums[:]      # Get a slice of the whole list; prints ["0, 1, 2, 3, 4]"
print nums[:-1]    # Slice indices can be negative; prints ["0, 1, 2, 3]"
nums[2:4] = [8, 9] # Assign a new sublist to a slice
print nums         # Prints "[0, 1, 8, 9, 4]"
```

### Comprehensions | 变换

Python 中同样可以使用 map, reduce, filter，其中 map 用于变换数组

```py
# 使用 map 对数组中的每个元素计算平方
items = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, items))

# map 支持函数以数组方式连接使用
def multiply(x):
    return (x*x)

def add(x):
    return (x+x)

funcs = [multiply, add]

for i in range(5):
    value = list(map(lambda x: x(i), funcs))
    print(value)
```

reduce 用于进行归纳计算

```py
# reduce 将数组中的值进行归纳
from functools import reduce
product = reduce((lambda x, y: x * y), [1, 2, 3, 4])

# Output: 24
```

filter 则可以对数组进行过滤

```py
number_list = range(-5, 5)
less_than_zero = list(filter(lambda x: x < 0, number_list))
print(less_than_zero)

# Output: [-5, -4, -3, -2, -1]
```

## 字典类型

### 创建增删

```py
d = {'cat': 'cute', 'dog': 'furry'}  # 创建新的字典
print d['cat']       # 字典不支持点(Dot)运算符取值
```

如果需要合并两个或者多个字典类型：

```py
# python 3.5
z = {**x, **y}

# python 2.7
def merge_dicts(*dict_args):
    """
    Given any number of dicts, shallow copy and merge into a new dict,
    precedence goes to key value pairs in latter dicts.
    """
    result = {}
    for dictionary in dict_args:
        result.update(dictionary)
    return result
```

### 索引遍历

可以根据键来直接进行元素访问

```py
# Python 中对于访问不存在的键会抛出 KeyError 异常，需要先行判断或者使用 get
print 'cat' in d     # Check if a dictionary has a given key; prints "True"

# 如果直接使用 [] 来取值，需要先确定键的存在，否则会抛出异常
print d['monkey']  # KeyError: 'monkey' not a key of d

# 使用 get 函数则可以设置默认值
print d.get('monkey', 'N/A')  # Get an element with a default; prints "N/A"
print d.get('fish', 'N/A')    # Get an element with a default; prints "wet"

d.keys() # 使用 keys 方法可以获取所有的键
```

Python 还提供了部分特殊的字典类型：

```py
from collections import OrderedDict, Counter
# Remembers the order the keys are added!
x = OrderedDict(a=1, b=2, c=3)
# Counts the frequency of each character
y = Counter("Hello World!")
```

可以使用 for-in 来遍历数组

```py
# 遍历键
for key in d:

# 比前一种方式慢
for k in dict.keys(): ...

# 直接遍历值
for value in dict.itervalues(): ...

# Python 2.x 中遍历键值
for key, value in d.iteritems():

# Python 3.x 中遍历键值
for key, value in d.items():
```

## 其他序列类型

### Set

```py
# Same as {"a", "b","c"}
normal_set = set(["a", "b","c"])

# Adding an element to normal set is fine
normal_set.add("d")

# 判断 Set 大小
len(s)

# 判断元素是否存在于 Set 中
x in s
x not in s

# 集合间运算符
s.issubset(t)
s.issuperset(t)
s.union(t)
s.intersection(t)
s.difference(t)
s.symmetric_difference(t)
```

```py
# A frozen set
frozen_set = frozenset(["e", "f", "g"])

print("Frozen Set")
print(frozen_set)

# Uncommenting below line would cause error as
# we are trying to add element to a frozen set
# frozen_set.add("h")
```

### Tuple

```py
# 修改 Tuple 中的值
t = ('275', '54000', '0.0', '5000.0', '0.0')
lst = list(t)
lst[0] = '300'
t = tuple(lst)
```

### Enum | 枚举类型

```py
class Enum(set):
    def __getattr__(self, name):
        if name in self:
            return name
        raise AttributeError
```

# 函数

## 函数定义

Python 中的函数使用 def 关键字进行定义，譬如

```py
def sign(x):
    if x > 0:
        return 'positive'
    elif x < 0:
        return 'negative'
    else:
        return 'zero'


for x in [-1, 0, 1]:
    print sign(x)
# Prints "negative", "zero", "positive"
```

Python 支持运行时创建动态函数，也即是所谓的 lambda 函数：

```py
def f(x): return x**2

# 等价于
g = lambda x: x**2
```

lambda 表达式是 Python 函数式开发的重要基石，其方便实现 Partial Function 等模式；典型的 lambda 函数声明如下：

```python
lambda x: x**2 + 2*x - 5
```

典型的用法譬如自定义的 filter 函数中：

```python
mult3 = filter(lambda x: x % 3 == 0, [1, 2, 3, 4, 5, 6, 7, 8, 9])
```

```python
def filterfunc(x):
    return x % 3 == 0
mult3 = filter(filterfunc, [1, 2, 3, 4, 5, 6, 7, 8, 9])

mult3 = [x for x in [1, 2, 3, 4, 5, 6, 7, 8, 9] if x % 3 == 0]

range(3,10,3)
```

## 参数

### 默认参数

### Option Arguments | 不定参数

```py
def example(a, b=None, *args, **kwargs):
  print a, b
  print args
  print kwargs

example(1, "var", 2, 3, word="hello")
# 1 var
# (2, 3)
# {'word': 'hello'}

a_tuple = (1, 2, 3, 4, 5)
a_dict = {"1":1, "2":2, "3":3}
example(1, "var", *a_tuple, **a_dict)
# 1 var
# (1, 2, 3, 4, 5)
# {'1': 1, '2': 2, '3': 3}
```

对于不定参数的调用，同样可以使用 `**` 运算符：

```py
func(**{'type':'Event'})

# 等价于
func(type='Event')
```

## 生成器

```py
def simple_generator_function():
    yield 1
    yield 2
    yield 3

for value in simple_generator_function():
    print(value)

# 输出结果
# 1
# 2
# 3
our_generator = simple_generator_function()
next(our_generator)
# 1
next(our_generator)
# 2
next(our_generator)
#3

# 生成器典型的使用场景譬如无限数组的迭代
def get_primes(number):
    while True:
        if is_prime(number):
            yield number
        number += 1
```

## 装饰器

装饰器是非常有用的设计模式

```py
# 简单装饰器

from functools import wraps
def decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print('wrap function')
        return func(*args, **kwargs)
    return wrapper

@decorator
def example(*a, **kw):
    pass

example.__name__  # attr of function preserve
# 'example'
# Decorator

# 带输入值的装饰器

from functools import wraps
def decorator_with_argument(val):
  def decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
      print "Val is {0}".format(val)
      return func(*args, **kwargs)
    return wrapper
  return decorator

@decorator_with_argument(10)
def example():
  print "This is example function."

example()
# Val is 10
# This is example function.

# 等价于

def example():
  print "This is example function."

example = decorator_with_argument(10)(example)
example()
# Val is 10
# This is example function.
```

# 类与对象

## 类定义

Python 中对于类的定义也很直接

```py
class Greeter(object):

    # Constructor
    def __init__(self, name):
        self.name = name  # Create an instance variable

    # Instance method
    def greet(self, loud=False):
        if loud:
            print 'HELLO, %s!' % self.name.upper()
        else:
            print 'Hello, %s' % self.name

g = Greeter('Fred')  # Construct an instance of the Greeter class
g.greet()            # Call an instance method; prints "Hello, Fred"
g.greet(loud=True)   # Call an instance method; prints "HELLO, FRED!"
```

### Managed Attributes | 受控属性

```py
# property、setter、deleter 可以用于复写点方法

class Example(object):
    def __init__(self, value):
       self._val = value

    @property
    def val(self):
        return self._val

    @val.setter
    def val(self, value):
        if not isintance(value, int):
            raise TypeError("Expected int")
        self._val = value

    @val.deleter
    def val(self):
        del self._val

    @property
    def square3(self):
        return 2**3

ex = Example(123)
ex.val = "str"
# Traceback (most recent call last):
#   File "", line 1, in
#   File "test.py", line 12, in val
#     raise TypeError("Expected int")
# TypeError: Expected int
```

### 类方法与静态方法

```py
class example(object):

  @classmethod
  def clsmethod(cls):
    print "I am classmethod"

  @staticmethod
  def stmethod():
    print "I am staticmethod"

  def instmethod(self):
    print "I am instancemethod"

ex = example()
ex.clsmethod()
# I am classmethod
ex.stmethod()
# I am staticmethod
ex.instmethod()
# I am instancemethod
example.clsmethod()
# I am classmethod
example.stmethod()
# I am staticmethod
example.instmethod()
# Traceback (most recent call last):
#   File "", line 1, in
# TypeError: unbound method instmethod() ...
```

如果我们希望直接比较两个对象的，则需要覆写该类的比较相关方法：

```py

class Thing:
    def __init__(self, value):
        self.__value = value
    def __gt__(self, other):
        return self.__value > other.__value
    def __lt__(self, other):
        return self.__value < other.__value
something = Thing(100)
nothing = Thing(0)
# True
something > nothing
# False
something < nothing
# Error
something + nothing
```

### 抽象类

Python 中支持定义抽象类，抽象类不可被直接实例化；抽象类必须包含一或多个抽象方法：

```py
from abc import ABC, abstractmethod

class AbstractClassExample(ABC):

    def __init__(self, value):
        self.value = value
        super().__init__()

    @abstractmethod
    def do_something(self):
        pass
```

在 Python 3 中，也可以通过继承元类的方式来实现:

```py
from abc import ABCMeta

class MyABC(metaclass=ABCMeta):
    pass
```

### MetaClass | 元类

Python 中所谓的

## 类继承

```py
# 父类必须继承 object 或者其他父类
class BaseClass(object):
    def __init__(self, *args, **kwargs):
        pass

class ChildClass(BaseClass):
    def __init__(self, *args, **kwargs):
        # 调用父类构造函数
        super(ChildClass, self).__init__(*args, **kwargs)
```

```py
class Car(object):
    condition = "new"

    def __init__(self, model, color, mpg):
        self.model = model
        self.color = color
        self.mpg   = mpg

class ElectricCar(Car):
    def __init__(self, battery_type, model, color, mpg):
        self.battery_type=battery_type
        super(ElectricCar, self).__init__(model, color, mpg)

car = ElectricCar('battery', 'ford', 'golden', 10)
print car.__dict__
```

## 对象

### 实例化

```py
class Foo(object):
    def __init__(self, a, b):
        self.a = a
        self.b = b

    def bar(self):
        pass

i = Foo(2, 3)
```

Python 中与类实例化相关的方法有 `__new__` 与 `__init__`，`__new__` 会在对象创建时候调用，覆写该方法能够自定义实例的创建过程；而 `__init__` 方法则是在实例创建完毕后初始化实例:

```py
class Foo(object):
    def __new__(cls, *args, **kwargs):
        print "Creating Instance"
        instance = super(Foo, cls).__new__(cls, *args, **kwargs)
        # 或者
        # object.__new__(cls, *args, **kwargs)
        return instance
    ...

>>> i = Foo(2, 3)
Creating Instance
```

### 属性操作

Python 中对象的属性不同于字典键，可以使用点运算符取值，直接使用 in 判断会存在问题

```py
class A(object):
    @property
    def prop(self):
        return 3

a = A()
print "'prop' in a.__dict__ =", 'prop' in a.__dict__
print "hasattr(a, 'prop') =", hasattr(a, 'prop')
print "a.prop =", a.prop

# 'prop' in a.__dict__ = False
# hasattr(a, 'prop') = True
# a.prop = 3
```

建议使用 hasattr, getattr, setattr 这种方式对于对象属性进行操作

```py
class Example(object):
  def __init__(self):
    self.name = "ex"
  def printex(self):
    print "This is an example"


# Check object has attributes
# hasattr(obj, 'attr')
ex = Example()
hasattr(ex,"name")
# True
hasattr(ex,"printex")
# True
hasattr(ex,"print")
# False

# Get object attribute
# getattr(obj, 'attr')
getattr(ex,'name')
# 'ex'

# Set object attribute
# setattr(obj, 'attr', value)
setattr(ex,'name','example')
ex.name
# 'example'
```

### 单例模式

我们可以通过覆写 `__new__` 方法或者创建特殊的 MetaClass 来实现单例模式:

```py
class Singleton(object):
    _instance = None  # Keep instance reference

    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = object.__new__(cls, *args, **kwargs)
        return cls._instance

# 指定数目的单例
class LimitedInstances(object):
    _instances = []  # Keep track of instance reference
    limit = 5

    def __new__(cls, *args, **kwargs):
        if not len(cls._instances) <= cls.limit:
            raise RuntimeError, "Count not create instance. Limit %s reached" % cls.limit
        instance = object.__new__(cls, *args, **kwargs)
        cls._instances.append(instance)
        return instance

    def __del__(self):
        # Remove instance from _instances
        self._instance.remove(self)
```

也可以通过继承元类的方式来实现:

```py
class Singleton(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super(Singleton,                                      cls).__call__(*args, **kwargs)
        return cls._instances[cls]


class SingletonClass(metaclass=Singleton):
    pass
class RegularClass():
    pass
x = SingletonClass()
y = SingletonClass()
print(x == y)
x = RegularClass()
y = RegularClass()
print(x == y)
```

# 异常与测试

## 异常处理

### try

```py
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
```

```py
class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")
```

### Context Manager - with

with 常用于打开或者关闭某些资源

```py
host = 'localhost'
port = 5566
with Socket(host, port) as s:
    while True:
        conn, addr = s.accept()
        msg = conn.recv(1024)
        print msg
        conn.send(msg)
        conn.close()
```

## 单元测试

```py
from __future__ import print_function

import unittest

def fib(n):
    return 1 if n<=2 else fib(n-1)+fib(n-2)

def setUpModule():
        print("setup module")
def tearDownModule():
        print("teardown module")

class TestFib(unittest.TestCase):

    def setUp(self):
        print("setUp")
        self.n = 10
    def tearDown(self):
        print("tearDown")
        del self.n
    @classmethod
    def setUpClass(cls):
        print("setUpClass")
    @classmethod
    def tearDownClass(cls):
        print("tearDownClass")
    def test_fib_assert_equal(self):
        self.assertEqual(fib(self.n), 55)
    def test_fib_assert_true(self):
        self.assertTrue(fib(self.n) == 55)

if __name__ == "__main__":
    unittest.main()
```

# 存储

## 文件读写

### 路径处理

Python 内置的 `__file__` 关键字会指向当前文件的相对路径，可以根据它来构造绝对路径，或者索引其他文件

```py
# 获取当前文件的相对目录
dir = os.path.dirname(__file__) # src\app

## once you're at the directory level you want, with the desired directory as the final path node:
dirname1 = os.path.basename(dir)
dirname2 = os.path.split(dir)[1] ## if you look at the documentation, this is exactly what os.path.basename does.

# 获取当前代码文件的绝对路径，abspath 会自动根据相对路径与当前工作空间进行路径补全
os.path.abspath(os.path.dirname(__file__)) # D:\WorkSpace\OWS\tool\ui-tool-svn\python\src\app

# 获取当前文件的真实路径
os.path.dirname(os.path.realpath(__file__)) # D:\WorkSpace\OWS\tool\ui-tool-svn\python\src\app

# 获取当前执行路径
os.getcwd()
```

可以使用 listdir、walk、glob 模块来进行文件枚举与检索：

```py
# 仅列举所有的文件
from os import listdir
from os.path import isfile, join
onlyfiles = [f for f in listdir(mypath) if isfile(join(mypath, f))]

# 使用 walk 递归搜索
from os import walk

f = []
for (dirpath, dirnames, filenames) in walk(mypath):
    f.extend(filenames)
    break

# 使用 glob 进行复杂模式匹配
import glob
print(glob.glob("/home/adam/*.txt"))
# ['/home/adam/file1.txt', '/home/adam/file2.txt', .... ]
```

### 简单文件读写

```py
# 可以根据文件是否存在选择写入模式
mode = 'a' if os.path.exists(writepath) else 'w'

# 使用 with 方法能够自动处理异常
with open("file.dat",mode) as f:
    f.write(...)
    ...
    # 操作完毕之后记得关闭文件
    f.close()

# 读取文件内容
message = f.read()
```

## 复杂格式文件

### JSON

```py
import json

# Writing JSON data
with open('data.json', 'w') as f:
     json.dump(data, f)

# Reading data back
with open('data.json', 'r') as f:
     data = json.load(f)
```

### XML

我们可以使用 [lxml](http://lxml.de/parsing.html) 来解析与处理 XML 文件，本部分即对其常用操作进行介绍。lxml 支持从字符串或者文件中创建 Element 对象：

```py
from lxml import etree

# 可以从字符串开始构造
xml = '<a xmlns="test"><b xmlns="test"/></a>'
root = etree.fromstring(xml)
etree.tostring(root)
# b'<a xmlns="test"><b xmlns="test"/></a>'

# 也可以从某个文件开始构造
tree = etree.parse("doc/test.xml")

# 或者指定某个 baseURL
root = etree.fromstring(xml, base_url="http://where.it/is/from.xml")
```

其提供了迭代器以对所有元素进行遍历：

```py
# 遍历所有的节点
for tag in tree.iter():
    if not len(tag):
        print tag.keys() # 获取所有自定义属性
        print (tag.tag, tag.text) # text 即文本子元素值

# 获取 XPath
for e in root.iter():
    print tree.getpath(e)
```

lxml 支持以 XPath 查找元素，不过需要注意的是，XPath 查找的结果是数组，并且在包含命名空间的情况下，需要指定命名空间：

```py
root.xpath('//page/text/text()',ns={prefix:url})

# 可以使用 getparent 递归查找父元素
el.getparent()
```

lxml 提供了 insert、append 等方法进行元素操作：

```py
# append 方法默认追加到尾部
st = etree.Element("state", name="New Mexico")
co = etree.Element("county", name="Socorro")
st.append(co)

# insert 方法可以指定位置
node.insert(0, newKid)
```

### Excel

可以使用 [xlrd]() 来读取 Excel 文件，使用 [xlsxwriter](http://xlsxwriter.readthedocs.io/) 来写入与操作 Excel 文件。

```py
# 读取某个 Cell 的原始值
sh.cell(rx, col).value
```

```py
# 创建新的文件
workbook = xlsxwriter.Workbook(outputFile)
worksheet = workbook.add_worksheet()

# 设置从第 0 行开始写入
row = 0

# 遍历二维数组，并且将其写入到 Excel 中
for rowData in array:
    for col, data in enumerate(rowData):
        worksheet.write(row, col, data)
    row = row + 1

workbook.close()
```

## 文件系统

对于高级的文件操作，我们可以使用 Python 内置的 shutil

```py
# 递归删除 appName 下面的所有的文件夹
shutil.rmtree(appName)
```

# 网络交互

## Requests

[Requests](https://parg.co/UrO) 是优雅而易用的 Python 网络请求库

```py
import requests

r = requests.get('https://api.github.com/events')
r = requests.get('https://api.github.com/user', auth=('user', 'pass'))

r.status_code
# 200
r.headers['content-type']
# 'application/json; charset=utf8'
r.encoding
# 'utf-8'
r.text
# u'{"type":"User"...'
r.json()
# {u'private_gists': 419, u'total_private_repos': 77, ...}

r = requests.put('http://httpbin.org/put', data = {'key':'value'})
r = requests.delete('http://httpbin.org/delete')
r = requests.head('http://httpbin.org/get')
r = requests.options('http://httpbin.org/get')
```

# 数据存储

## MySQL

```py
import pymysql.cursors

# Connect to the database
connection = pymysql.connect(host='localhost',
                             user='user',
                             password='passwd',
                             db='db',
                             charset='utf8mb4',
                             cursorclass=pymysql.cursors.DictCursor)

try:
    with connection.cursor() as cursor:
        # Create a new record
        sql = "INSERT INTO `users` (`email`, `password`) VALUES (%s, %s)"
        cursor.execute(sql, ('webmaster@python.org', 'very-secret'))

    # connection is not autocommit by default. So you must commit to save
    # your changes.
    connection.commit()

    with connection.cursor() as cursor:
        # Read a single record
        sql = "SELECT `id`, `password` FROM `users` WHERE `email`=%s"
        cursor.execute(sql, ('webmaster@python.org',))
        result = cursor.fetchone()
        print(result)
finally:
    connection.close()
```

# 并发编程

concurrent.futures 是标准库的一部分，自 3.2 版本之后引入；对于老版本则需要手动引入 futures 依赖库。我们可以使用 ProcessPoolExecutor 来处理 CPU 密集型任务，使用 ThreadPoolExecutor 来处理网络操作或者 IO 操作。ProcessPoolExecutor 内部使用了 multiprocessing 模块，其不会受到 GIL(Global Intercept Lock)的干扰。

```py
from concurrent.futures import ThreadPoolExecutor
import time

import requests

def fetch(a):
    url = 'http://httpbin.org/get?a={0}'.format(a)
    r = requests.get(url)
    result = r.json()['args']
    return result

start = time.time()

# if max_workers is None or not given, it will default to the number of processors, multiplied by 5
with ThreadPoolExecutor(max_workers=None) as executor:
    for result in executor.map(fetch, range(30)):
        print('response: {0}'.format(result))

print('time: {0}'.format(time.time() - start))
```

executor.submit() 则可以返回 Future 对象，所谓的 Future 即是包含了某个异步执行函数，并且会在未来执行完毕或者抛出异常的对象。而 as_completed 函数与上文使用的 map 函数的区别在于，map 会按照传入迭代器的顺序返回结果，而 as_completed 则会返回首页执行完毕的 Future 对象：

```py
from concurrent.futures import ThreadPoolExecutor, as_completed

import requests

def fetch(url, timeout):
    r = requests.get(url, timeout=timeout)
    data = r.json()['args']
    return data

with ThreadPoolExecutor(max_workers=10) as executor:
    futures = {}
    for i in range(42):
        url = 'https://httpbin.org/get?i={0}'.format(i)
        future = executor.submit(fetch, url, 60)
        futures[future] = url

    for future in as_completed(futures):
        url = futures[future]
        try:
            data = future.result()
        except Exception as exc:
            print(exc)
        else:
            print('fetch {0}, get {1}'.format(url, data))
```

# 编程规范

```py
def fetch_bigtable_rows(big_table, keys, other_silly_variable=None):
    """Fetches rows from a Bigtable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by big_table.  Silly things may happen if
    other_silly_variable is not None.

    Args:
        big_table: An open Bigtable Table instance.
        keys: A sequence of strings representing the key of each table row
            to fetch.
        other_silly_variable: Another optional variable, that has a much
            longer name than the other args, and which does nothing.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {'Serak': ('Rigel VII', 'Preparer'),
         'Zim': ('Irk', 'Invader'),
         'Lrrr': ('Omicron Persei 8', 'Emperor')}

        If a key from the keys argument is missing from the dictionary,
        then that row was not found in the table.

    Raises:
        IOError: An error occurred accessing the bigtable.Table object.
    """
    pass
```

所谓"内部(Internal)"表示仅模块内可用, 或者, 在类内是保护或私有的。用单下划线(`_`)开头表示模块变量或函数是 protected 的(使用 `import * from` 时不会包含)。用双下划线(`__`)开头的实例变量或方法表示类内私有。将相关的类和顶级函数放在同一个模块里. 不像 Java, 没必要限制一个类一个模块。对类名使用大写字母开头的单词(如 CapWords, 即 Pascal 风格), 但是模块名应该用小写加下划线的方式(如 lower_with_under.py). 尽管已经有很多现存的模块使用类似于 CapWords.py 这样的命名, 但现在已经不鼓励这样做, 因为如果模块名碰巧和类名一致, 这会让人困扰.

| Type                       | Public             | Internal                                                             |
| -------------------------- | ------------------ | -------------------------------------------------------------------- |
| Modules                    | lower_with_under   | `_lower_with_under`                                                  |
| Packages                   | lower_with_under   |                                                                      |
| Classes                    | CapWords           | `_CapWords`                                                          |
| Exceptions                 | CapWords           |                                                                      |
| Functions                  | lower_with_under() | \_lower_with_under()                                                 |
| Global/Class Constants     | CAPS_WITH_UNDER    | `_CAPS_WITH_UNDER`                                                   |
| Global/Class Variables     | lower_with_under   | `_lower_with_under `                                                 |
| Instance Variables         | lower_with_under   | \_lower_with_under (protected) or \_\_lower_with_under (private)     |
| Method Names               | lower_with_under() | \_lower_with_under() (protected) or \_\_lower_with_under() (private) |
| Function/Method Parameters | lower_with_under   |                                                                      |
| Local Variables            | lower_with_under   |                                                                      |

# Links

- https://mojotv.cn/2018/12/26/python-cheat-sheet Python快速入门和查询 