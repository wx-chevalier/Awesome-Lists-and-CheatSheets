# Ruby CheatSheet

# 数据结构

## 变量

### 类型判断

```ruby
>> s = "something"
=> "something"
>> s.kind_of?(Array)
=> false
>> s = ["something", "else"]
=> ["something", "else"]
>> s.kind_of?(Array)
=> true
```

# 类与对象

## 成员变量(Variable)

### Class Variable

### Instance Variable

# 常用操作(Common APIs)

## IO

### File

#### Read

```
def read_from_file(file_name)
  # read file and get content as list
  file_list = []
  file = File.open(file_name)
  file.each {
      |line|
    if (line != "\n")
      file_list << line.chomp
    end
  }
  return file_list
end
```

Introduce
程序块代码文件编码

# encoding: UTF-8

QuickStart
Installer
Ubuntu

1.  首先在使用 apt-get 之前，必须先 update 一下，否则有些库是安装不上的。
    [plain] view plaincopyprint?
1.  $ sudo apt-get update
    $ sudo apt-get update
    [plain] view plaincopyprint?
1.  $ sudo apt-get install -y build-essential openssl curl libcurl3-dev libreadline6 libreadline6-dev git zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev libxslt-dev autoconf automake libtool imagemagick libmagickwand-dev libpcre3-dev libsqlite3-dev libmysql-ruby libmysqlclient-dev
    $ sudo apt-get install -y build-essential openssl curl libcurl3-dev libreadline6 libreadline6-dev git zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev libxslt-dev autoconf automake libtool imagemagick libmagickwand-dev libpcre3-dev libsqlite3-dev libmysql-ruby libmysqlclient-dev
     2. 安装 RVM
    [html] view plaincopyprint?
1.  $ curl -L https://get.rvm.io | bash -s stable
    $ curl -L https://get.rvm.io | bash -s stable
      下面这步是不行的，要 logout 再次登录
    [plain] view plaincopyprint?
1.  $ source ~/.rvm/scripts/rvm
    $ source ~/.rvm/scripts/rvm
    然后就安装好 rvm 了
    [plain] view plaincopyprint?
1.  \$ rvm -v
1.  rvm install 2.2.1
1.  \$ gem source -r https://rubygems.org/
1.  \$ gem source -a http://ruby.taobao.org

数据结构变量
Ruby 中常用的内置的变量对象种类有：对象类
数值
Numeric
字符串
String
数组
Array
哈希
Hash
正则表达式
Regex
文件
File
符号
Symbol

命名
Ruby 中常用的变量类型有：局部变量：以英文字母或者\_开头全局变量：以\$开头实例变量：以@开头类变量：以@@开头赋值常量保留字类型判断基本数据类型空值
String
长度
array.size
names = [1,2,3,4,5]
p names.size
空判断

创建增删
.连接
.删除

指定字符删除
str.delete([other_str]+) => new_str
"hello".delete "l","lo" #=> "heo"
"hello".delete "lo" #=> "he"
"hello".delete "aeiou", "^e" #=> "hell"
"hello".delete "ej-m" #=> "ho"
指定下标删除
str(1..2) = ""
空白字符删除
str.lstrip => new_str
" hello ".lstrip #=> "hello "、
"hello".lstrip #=> "hello"
"hello".chomp #=> "hello"
"hello\n".chomp #=> "hello"
"hello\r\n".chomp #=> "hello"
"hello\n\r".chomp #=> "hello\n"
"hello\r".chomp #=> "hello"
"hello".chomp("llo") #=> "he"
"string\r\n".chop #=> "string"
"string\n\r".chop #=> "string\n"
"string\n".chop #=> "string"
"string".chop #=> "strin"

索引遍历
.匹配匹配判断
/模式/ =~ 希望匹配的字符串存在则返回匹配部分的位置，否则返回 nil。匹配查找
.截取下标截取
s = "hello"s[2..3] # "ll": 位于索引 2 到 3 的字符 s[-3..-1] # "llo": 负数索引页可以使用 s[0..0] # "h": Range 只包含一个字符 s[0...0] # "": 空的 Range 对象 s[2..1] # "": 这也是空的 Ranges[7..10] # nil: 这个 Range 超出了索引范围，所以返回 nils[-2..-1] = "p!" # 替换值，现在 s=="help!"s[0...0] = "Please " # 在起始位置插入新值，现在 s== "Please help!"s[6..10] = "" # 删除值，现在 s== "Please!"

统计操作其他操作字符串反转
str.reverse => new_str"stressed".reverse  
#=> "desserts"

Array
长度
array.size
names = [1,2,3,4,5]
p names.size
空判断

创建增删
.1 创建数组的创建方式可以有：(1)赋值创建
names = [] 或者 names = [“I”,”Love”,”Ruby”]
类初始化拷贝创建

.2 添加
a = [1,2,3,4]
a << 5 # [1,2,3,4,5]
a << [5] #[1,2,3,4,[5]]
a.concat([5]) #[1,2,3,4,5]
.3 删除
Array.compact!
删除 nil 元素

delete 删除元素，如果元素重复，全部删除 a = [ "a", "b", "b", "b", "c" ]
a.delete("b")
puts a => ["a","c"]
delete_at

删除 pos 所指位置的元素并返回它。若 pos 超出数

组范围则返回 nil a = %w( ant bat cat dog )
a.delete_at(2) ? "cat"
a=> ["ant", "bat", "dog"]

a.delete_at(99) => nil
delete_if 根据条件删除 a = [ "a", "b", "c" ]
a.delete_if {|x| x >= "b" } => ["a"]

栈列操作
索引遍历
.1 索引下标索引存在性判断索引反查
.2 遍历变量遍历索引遍历迭代器遍历数组.each do |变量|
希望循环的处理
end
Or
数组.each {
|变量|
希望循环的处理
}
.3 匹配
.4 截取统计操作
.1 排序
.2 筛选
.3 去重

1.  arr = [1,1,2,3]
    b = arr & arr
    b => [1,2,3]
2.  arr = [1,1,2,3]
    b = arr.uniq
    b => [1,2,3]

Hash
Hash 即是其他语言中常见的字典类型。长度
h.size
h.length

空判断
h.empty?

创建增删

索引遍历
.1 索引判断键值是否存在。
h.key?(key)

h.has_key?(key)

h.include?(key)

h.member?(key)

.2 遍历变量遍历索引遍历迭代器遍历
hash.each{|key,value| doSomething}
Others
TimeDate
流程控制运算符条件判断循环
for
下标索引遍历：
for i in from..to do #do 可以省略
doSomething
end
迭代器
class TrafficLight  
 include Enumerable
end
each
select

> > [1,2,3,4,5].select { |i| i > 3 }
> > => [4,5]
> > reject
> > 函数

序列操作
map/reduce
(1..5).reduce { |sum,num| sum = sum \* num }
Modules
Ruby 中要引用一个第三方文件作为库，可以使用 require 关键字，即：
require 希望使用的库名注意，在 require 的引用中可以省略.rb 这个后缀名

Class&Object
方法类别
Ruby 在调用方法时可以省略()。类方法(Instance Method)实例方法(Instance Method)异常处理
Common APIs
IO
Console
Output
print
print “Hello, Ruby!”
puts
末尾一定会带有换行。
p
对于字符串或者数值类型会有不同的输出表示。
Math
Regexp

# MiniTest

- [Github 上 MiniTest 的主页][1]

## UnitTest

- 待测试类

```ruby
class Meme
  def i_can_has_cheezburger?
    "OHAI!"
  end

  def will_it_blend?
    "YES!"
  end
end
```

- 测试类

```ruby
require "minitest/autorun"

class TestMeme < Minitest::Test
  def setup
    @meme = Meme.new
  end

  def test_that_kitty_can_eat
    assert_equal "OHAI!", @meme.i_can_has_cheezburger?
  end

  def test_that_it_will_not_blend
    refute_match /^no/i, @meme.will_it_blend?
  end

  def test_that_will_be_skipped
    skip "test this later"
  end
end
```

- 运行测试直接运行 `ruby people_test.rb`即可得到结果

```
Run options: --seed 10922
# Running:
.
Finished in 0.001302s, 768.0492 runs/s, 768.0492 assertions/s.

1 runs, 1 assertions, 0 failures, 0 errors, 0 skips
```

## Specs

```
require "minitest/autorun"

describe Meme do
  before do
    @meme = Meme.new
  end

  describe "when asked about cheeseburgers" do
    it "must respond positively" do
      @meme.i_can_has_cheezburger?.must_equal "OHAI!"
    end
  end

  describe "when asked about blending possibilities" do
    it "won't say no" do
      @meme.will_it_blend?.wont_match /^no/i
    end
  end
end
```

## Benchmarks

- 添加到 UnitTest 中

```
# optionally run benchmarks, good for CI-only work!
require "minitest/benchmark" if ENV["BENCH"]

class TestMeme < Minitest::Benchmark
  # Override self.bench_range or default range is [1, 10, 100, 1_000, 10_000]
  def bench_my_algorithm
    assert_performance_linear 0.9999 do |n| # n is a range value
      @obj.my_algorithm(n)
    end
  end
end
```

- 添加到 Specs 中

```
describe "Meme Benchmark" do
  if ENV["BENCH"] then
    bench_performance_linear "my_algorithm", 0.9999 do |n|
      100.times do
        @obj.my_algorithm(n)
      end
    end
  end
end
```

# RSpec

- [rspec 入门教程][2]

## Quick Start

In the project directory of the Ruby project that we have just created, create a Gemfile with the following content:

```
source 'https://rubygems.org'
gem 'rspec', :require => false, :group => :test
```

Next, create a folder named spec and a new file named `spec_helper.rb`. Add the following into `spec_helper.rb`:

```
require_relative '../string_ops'
```

Ideally, we will have one spec file per Ruby class, all of the spec files will reside in this spec folder, and each of them will have require 'spec_helper' in their first line.In our case, we want to write some tests for the StringOps Ruby class, we do this by first creating the file string_ops_spec.rb in the spec folder and add the following into the file:

```
require 'spec_helper'

describe StringOps do
  string_ops = StringOps.new
  input_string = "To see a World in a Grain of Sand, And a Heaven in a Wild Flower, Hold Infinity in the palm of your hand, And Eternity in an hour."

  describe "#to_upper" do
    it "returns upper case for input_string" do
      expected_string = "TO SEE A WORLD IN A GRAIN OF SAND, AND A HEAVEN IN A WILD FLOWER, HOLD INFINITY IN THE PALM OF YOUR HAND, AND ETERNITY IN AN HOUR."
      expect(string_ops.to_upper(input_string)).to eq(expected_string)
    end
  end

  describe "#to_lower" do
    it "returns lower case for input_string" do
      expected_string = "to see a world in a grain of sand, and a heaven in a wild flower, hold infinity in the palm of your hand, and eternity in an hour."
      expect(string_ops.to_lower(input_string)).to eq(expected_string)
    end
  end
end
```

> `expect(string_ops.to_upper(input_string)).to eq(expected_string)`这是 rspec 内置的匹配器。[这里是关于匹配器的列表][3]

在配置完 rspec 之后，回退到项目的根目录然后可以使用`rspec spec`命令来进行 rspec 的测试。

```
$ rspec spec
..
Finished in 0.00109 seconds (files took 0.09191 seconds to load)
2 examples, 0 failures
```

上述命令会显示出总的测试数目与失败的测试的数目。也可以用--format 参数指定不同的输出格式，譬如：

```
$ rspec spec --format documentation

StringOps
  #toUpper
    returns upper case of input string
  #toLower
    returns lower case of input string

Finished in 0.00111 seconds (files took 0.08931 seconds to load)
2 examples, 0 failures
```

## Synatx

### 定义器

再 RSpec 中，用 describe、context 与 it 结合使用的方式来定义一个测试用例。

- describe
  我们用 describe()方法定义一个测试用例组，describe()方法的参数可以是我们要测试的对象(如例中的 People)，可以是一个字符串，用来描述该组，describe 方法后的字符串所描述的内容可以对应一个用户故事。注意 describe()方法是可以嵌套的，两个 describe()方法衔接起来可以更细化一个用户故事，如上边的里面的 describe()方法内就表示：”People have enough money pay for house”。
- context
  context 与 describe 都可以用于描述一个用户的故事，但是 describe 往往用于描述只执行一次的情况，而 context 用于描述可能存在多种情况的故事。

```ruby
describe "launch the rocket" do
  before(:each) do
    #prepare a rocket for all of the tests
    @rocket = Rocket.new
  end

  context "all ready" do
    before(:each) do
      #under the state of ready
      @rocket.ready = true
    end

    it "launch the rocket" do
      @rocket.launch().should be_true
    end
  end

  context "not ready" do
    before(:each) do
      #under the state of NOT ready
      @rocket.ready = false
    end

    it "does not launch the rocket" do
      @rocket.launch().should be_false
    end
  end
end
```

- it
  我们用 it()方法定义一个具体的测试用例(在 RSpec 中，称一个测试用例为一个 example)。其后的字符串为该方法的参数，用来描述一个具体的场景，it 方法体就是我们对系统在该场景下的行为的定义。It()方法和 describe()方法衔接起来，可以完整的描述一个系统行为，以上边的最后的一个测试用例为：”People have enough money pay for house should travel ”。

### 修饰器

这两个方法很多测试框架都支持，需要说明的是这两个方法的参数，例子中为符号’:each’，表明对于每一个测试用例，先执行 before()方法中的代码，用例完成后执行 after()方法中的代码，若参数为’:all’，则表示在所有的测试用例执行之前，先执行 before()方法中的代码，所有的用例完成后执行 after()方法中的代码。
RSpec 还提供 around()方法，暂不懂其用法，之后的报告中补上。帮助方法：所谓的帮助方法就是把多个测试用例中重复的操作抽出作为一个公用的方法，提高代码重用度。如例子中的 work_hard()方法。共享行为：系统的某一个行为是很多场景下都具有的，那么我们可以把它定义为一个共享行为，我们通过 share_examples_for()方法 定义共享行为，使用 it_behaves_like()方法共享定义过的系统行为，如例子中的 share_examples_for “any people”，it_behaves_like “any people”。

## Mocks

rspec 中另一个比较好的特性即是内置的 mock 特性，[rspec-mocks 主页][4]可以通过添加如下代码到 string_ops_spec.rb 文件中实现：
Stub - fake implementation of a method
Mock - fake implementation of an object
Double - a newer term to represent an object that stands in for another object

```
context "mock response" do
  it "mocks the response from to_upper" do
    mocked_response = "This is a mocked to_upper response."
    mocked_string_ops = double("mocked_string_ops")
    allow(mocked_string_ops).to receive(:to_upper).and_return(mocked_response)
    expect(mocked_string_ops.to_upper("any string")).to eq(mocked_response)
  end
end
```

他会模拟调用，结果如下：

```
$ rspec spec --format documentation

StringOps
  #toUpper
    returns upper case of input string
  #toLower
    returns lower case of input string
  mock response
    mocks the response from toUpper

Finished in 0.00559 seconds (files took 0.09207 seconds to load)
3 examples, 0 failures
```

# SimpleCov

Right, we have rspec as the testing tool in Ruby, so far so good, next, let’s look briefly into the code coverage analysis tool SimpleCov in Ruby.

To get started, include SimpleCov into the Gemfile.

```
source 'https://rubygems.org'

gem 'rspec', :require => false, :group => :test
gem 'simplecov', :require => false, :group => :test
```

Then, load and launch SimpleCov at the beginning of the spec/spec_helper.rb file:

```
require 'simplecov'
SimpleCov.start
require_relative '../string_ops'
```

Make sure that it’s added to the very beginning of the file before any of your application code is required, otherwise SimpleCov won’t be able to track the files and their coverage.

Next, run rspec like we normally would and that’s it, we have a coverage report generated,

```
$ rspec spec
...

Finished in 0.00556 seconds (files took 0.11402 seconds to load)
3 examples, 0 failures
Coverage report generated for RSpec to /a/b/c/project_dir/coverage. 6 / 7 LOC (85.71%) covered.
```

Notice the last line of the output says that the coverage report is generated, we can now open coverage/index.html in a browser to view it.
![enter description here][5]
We can see that there’s 85.71% of code coverage on string_ops.rb, if you click on the link, you will see the lines that were missed in the tests.
![enter description here][6]

[1]: https://github.com/seattlerb/minitest
[2]: http://www.jianshu.com/p/1db9ee327357
[3]: http://www.rubydoc.info/gems/rspec-expectations/frames
[4]: https://github.com/rspec/rspec-mocks
[5]: C:\wamp\www\md-repo\1429896390839.jpg "1429896390839.jpg"
[6]: C:\wamp\www\md-repo/1429896405807.jpg "1429896405807.jpg"
