[🔆 中文版本](./JavaScript-CheatSheet.md) | [☀️ English Version](./JavaScript-CheatSheet.en.md)

# JavaScript CheatSheet | 现代 JavaScript 语法速览与实战清单

JavaScript CheatSheet 是对于 JavaScript 学习/实践过程中的语法与技巧进行盘点，其属于 [Awesome CheatSheet](https://github.com/wx-chevalier/Awesome-CheatSheets/) 系列，致力于提升学习速度与研发效能，即可以将其当做速查手册，也可以作为轻量级的入门学习资料。本文参考了许多优秀的文章与代码示范，统一声明在了 [JavaScript Links](https://github.com/wx-chevalier/Awesome-Lists/blob/master/ProgrammingLanguage/JavaScript/JavaScript-List.md)；如果希望深入了解某方面的内容，可以继续阅读[]()，或者前往 [coding-snippets/javascript]() 查看使用 JavaScript 解决常见的数据结构与算法、设计模式、业务功能方面的代码实现。

Javascript 于 1995 年由网景公司的 Brendan Eich 发明。最初它作为一种简单的，用于开发网站的脚本语言而被发明出来，是用于开发复杂网站的 Java 的补充。但由于它与网页结合度很高并且在浏览器中得到内置的支持，所以在网页前端领域 Javascript 变得比 Java 更流行了。

对于 JavaScript 的语法速览可以参考本目录下的 [js-snippets](https://parg.co/QNv)。

# 基础语法

# 表达式与控制流

## 操作符

### 解构操作符

```js
let a;
{a} = {a:1}

// a = 1
```

某些场景下我们需要进行深层解构，同时保存某个浅层属性值：

```js
const {
  a,
  a: { b },
} = { a: { b: 1 } };

// a = {b:1}, b = 1
```

### 扩展操作符

扩展操作符(Spread Syntax)，即 ...，其允许某个将某个 Iterable 对象扩展到当前位置：

```js
const mid = [3, 4];
const arr = [1, 2, ...mid, 5, 6]; // [1, 2, 3, 4, 5, 6]

const arr = [2, 4, 8, 6, 0];
const max = Math.max(...arr); // 8

const str = "hello";
const chars = [...str]; // ["h", "e", "l", "l", "o"]
```

## 循环

for-of 循环，可作用在可迭代对象上，正是利用了可迭代对象上的默认迭代器。大致过程是：for-of 循环每执行一次都会调用可迭代对象的 next()方法，并将迭代器返回的结果对象的 value 属性存储在变量中，循环将继续执行这一过程直到返回对象的 done 属性的值为 true。

# 基本数据类型

JavaScript 内置了 6 种基础数据类型：Number, String, Boolean, null, undefined, Symbol:

```js
typeof 0; // number
typeof true; // boolean
typeof "Hello"; // string
typeof Math; // object
typeof null; // object  !!
typeof Symbol("Hi"); // symbol (New ES6)
```

## 类型判断与变量比较

### 隐式转换

```
// 0[object Object]1
{} + [] + {} + [1]

// NaN[object Object]
{} + [1,2] + {} + []
```

```js
// false，等式两侧存在 NaN，则为 false
NaN == NaN

// true, 先进行 Bool 操作转化为 false，然后两侧都变为数字 0
[] == ![]
```

## Number | 数值类型

JavaScript 中并没有区分整型或者浮点类型，而是统一使用 Number 表示。

JavaScript 内置的 Math 对象提供了极大极小的整型值以及多个数值类型的工具函数：

```js
value = Number.MAX_SAFE_INTEGER / 10; // 900719925474099.1
value = (Number.MAX_SAFE_INTEGER / 10) * -1; // -900719925474099.1

// 向下取整
let intvalue = Math.floor(floatvalue);
let intvalue = Math.ceil(floatvalue);
let intvalue = Math.round(floatvalue);

// `Math.trunc` was added in ECMAScript 6
let intvalue = Math.trunc(floatvalue);
```

## String | 字符串类型

```js
str.substr(start[, length])
"abc".substr(1,2) // bc

str.substring(indexStart[, indexEnd])
"abc".substring(1,2) // b
```

## Regex | 正则表达式

对于常量正则表达式，可以使用正则字符串方式；而对于动态的正则表达式，可以使用正则表达式构造函数

```js
// Regular Expression Literal
const regexLiteral = /cat/;

// Regular Expression Constructor
const regexConstructor = new RegExp("cat");

// 也可以将两个正则表达式合并为一个
const lower = new RegExp(/--RegexCode--/);
const upper = new RegExp(/--RegexCode--/);
const finalRe = new RegExp(lower.source + "|" + upper.source);
```

- Symbols

  - `.` —  匹配除了换行之外的任意字符
  - `^` —  匹配字符串的首部
  - `$` —  匹配字符串的末尾

- Number

  - `*` —  匹配前述的表达式零或多次
  - `+` —  匹配前述的表达式一或多次
  - `?` —  匹配前述的表达式零或一次
  - `a{3}` - 匹配指定数目的 a
  - `a{3,}` - 匹配不少于 3 个的 a
  - `a{3,6}` - 匹配 3 到 6 个 a

- Character groups

  - `\d` —  匹配任意的数值
  - `\w` —  匹配任意的字符
  - `[XYZ]` —  数组中任一值匹配，多范围混搭的话，可以使用 `[A-Z][xyz]+` 来匹配集合中的任一字符
  - `[^a-z]` — `^` 用于进行反选，这里即表示匹配非 a-z 字符的其他值；`([^B]*)` 表示该位置是除了 B 之外的任意值。

- Advanced

  - `(x)` —  捕获圆括号，匹配 x 并且记录捕获项
  - `(x|y)` - 匹配 x 或者 y
  - `(?:x)` —  非匹配圆括号，仅匹配而不记录
  - `x(?=y)` —  预测匹配，仅匹配那些 y 之前的 x

- Flags

  - `g` —  全局搜索
  - `i` —  大小写敏感搜索

### 匹配提取

正则表达式可以用来判断元素存在性，用于字符串替换等：

```js
const str1 = "the cat says meow";
const hasCat = /cat/;
hasCat.test(str1);
// true

function removeCc(str) {
  return str.replace(/([A-Z])/g, " $1");
}
removeCc("camelCase"); // 'camel Case'
removeCc("helloWorldItIsMe"); // 'hello World It Is Me'

// replace 支持回调函数，譬如用来将下划线转 camelCase
key.replace(/\_./g, (str) => str[1].toUpperCase());
```

较为常用的是 match 与 exec 方法，对于预设的捕获组，其会按序排列在 `match` 数组中。如果执行 exec 方法的正则表达式没有分组（没有括号括起来的内容），那么如果有匹配，他将返回一个只有一个元素的数组，这个数组唯一的元素就是该正则表达式匹配的第一个串; 如果没有匹配则返回 null。

```js
const someText = "web2.0 .net2.0";
const pattern = /(\w+)(\d)\.(\d)/g;
const outCome_exec = pattern.exec(someText);
// [ 'net2.0', 'net', '2', '0', index: 8, input: 'web2.0 .net2.0', groups: undefined ]
// 当 match 全局匹配时，会直接返回匹配列表
const outCome_match = someText.match(pattern);
// [ 'web2.0', 'net2.0' ]

// 提取匹配项
const s = '[description:"aoeu" uuid:"123sth"]';

const re = /\s*([^[:]+):\"([^"]+)"/g;
let m;
while ((m = re.exec(s))) {
  console.log(m[1], m[2]);
}

// 将字符串分割
"1234567890".match(/.{1,2}/g);
// ['12', '34', '56', '78', '90'];
```

exec 与 match 的区别在于，在全局匹配模式下，match 仅会返回匹配项数组，而忽略提取项；exec 会需要迭代调用才会返回全部结果:

```js
re_once = /([a-z])([A-Z])/;
re_glob = /([a-z])([A-Z])/g;

st = "aAbBcC";

console.log(
  "match once=" + st.match(re_once) + "  match glob=" + st.match(re_glob)
);
console.log(
  "exec once=" + re_once.exec(st) + "   exec glob=" + re_glob.exec(st)
);
console.log(
  "exec once=" + re_once.exec(st) + "   exec glob=" + re_glob.exec(st)
);
console.log(
  "exec once=" + re_once.exec(st) + "   exec glob=" + re_glob.exec(st)
);

/*
match once=aA,a,A  match glob=aA,bB,cC
exec once=aA,a,A   exec glob=aA,a,A
exec once=aA,a,A   exec glob=bB,b,B
exec once=aA,a,A   exec glob=cC,c,C
*/
```

### 匹配模式

`/g` 标识标识全局匹配。`/y` 标识(Sticky 模式)表示匹配必须从 `re.lastIndex`，即上一次匹配的末尾处开始，该行为类似于 `^` 标识，不过不强制从首部开始。

```js
const str = "#foo#";
const regex = /foo/y;

regex.lastIndex = 1;
regex.test(str); // true
regex.lastIndex = 5;
regex.test(str); // false (lastIndex is taken into account with sticky flag)
regex.lastIndex; // 0 (reset after match failure)
```

如下实例较好地对比了全局模式与严格模式的区别，严格模式并不会自动忽略中间的非匹配对象：

```js
function matcher(regex, input) {
  return () => {
    const match = regex.exec(input);
    const lastIndex = regex.lastIndex;
    return { lastIndex, match };
  };
}
const input = "haha haha haha";
const nextGlobal = matcher(/ha/g, input);
console.log(nextGlobal()); // <- { lastIndex: 2, match: ['ha'] }
console.log(nextGlobal()); // <- { lastIndex: 4, match: ['ha'] }
console.log(nextGlobal()); // <- { lastIndex: 7, match: ['ha'] }
const nextSticky = matcher(/ha/y, input);
console.log(nextSticky()); // <- { lastIndex: 2, match: ['ha'] }
console.log(nextSticky()); // <- { lastIndex: 4, match: ['ha'] }
console.log(nextSticky()); // <- { lastIndex: 0, match: null }
```

## DateTime | 时间与日期

基础的时间与日期知识参考 [Programming Language CheatSheet/时间与日期]()。

如果是轻量级的时间与日期操作，推荐使用 [date-fns](https://github.com/date-fns/date-fns)。

```js
new Date();
// Fri Aug 21 2015 15:51:55 GMT+0800 (中国标准时间)
new Date(1293879600000);
new Date("2011-01-01T11:00:00");
new Date("2011/01/01 11:00:00");
new Date(2011, 0, 1, 11, 0, 0);
new Date("jan 01 2011,11 11:00:00");
new Date("Sat Jan 01 2011 11:00:00");
// Sat Jan 01 2011 11:00:00 GMT+0800 (中国标准时间)
new Date("sss");
new Date("2011/01/01T11:00:00");
new Date("2011-01-01-11:00:00");
new Date("1293879600000");
// Invalid Date
new Date("2011-01-01T11:00:00") - new Date("1992/02/11 12:00:12");
// 596069988000
```

# 集合类型

## Array | 数组

### 创建

```js
// 创建一个数组
const arrayObj = new Array();

// 创建一个数组并指定长度，注意不是上限，是长度
const arrayObj = new Array([size]);

// 创建一个数组并赋值
const arrayObj = new Array([element0[, element1[, ...[, elementN]]]]);
```

也可以从类数组结构中创建出新的数组对象：

```js
const arrayLike = {
  0: "a",
  1: "b",
  length: 2,
  *[Symbol.iterator]() {
    yield this[1];
    yield this[0];
  },
};

console.log(Array.from(arrayLike));
```

```js
// 使用 Array.from 创建序列数组
Array.from({
  length: 100,
}).map((_, i) => i);
```

```js
const uniqueArray = (arr) => [...new Set(arr)];

uniqueArray([1, 2, 2, 3, 4, 4, 5]);
// [1,2,3,4,5]
```

### 索引与遍历

### 增删复制

数组元素的添加：

```js
// 将一个或多个新元素添加到数组结尾，并返回数组新长度
arrayObj.push([item1 [item2 [. . . [itemN ]]]]);

// 将一个或多个新元素添加到数组开始，数组中的元素自动后移，返回数组新长度
arrayObj.unshift([item1 [item2 [. . . [itemN ]]]]);

//将一个或多个新元素插入到数组的指定位置，插入位置的元素自动后移，返回""
arrayObj.splice(insertPos,0,[item1[, item2[, . . . [,itemN]]]]);
```

数组元素的删除：

```js
// 移除最后一个元素并返回该元素值
arrayObj.pop();

// 移除最前一个元素并返回该元素值，数组中元素自动前移
arrayObj.shift();

// 删除从指定位置deletePos开始的指定数量deleteCount的元素，数组形式返回所移除的元素
arrayObj.splice(deletePos, deleteCount);
```

数组的截取与合并：

```js
// 以数组的形式返回数组的一部分，注意不包括 end 对应的元素，如果省略 end 将复制 start 之后的所有元素
arrayObj.slice(start, [end]);

// 将多个数组（也可以是字符串，或者是数组和字符串的混合）连接为一个数组，返回连接好的新的数组
arrayObj.concat([item1[, item2[, . . . [,itemN]]]]);
```

### Transform | 变换

```js
// 异步 map 操作
await Promise.all(
  arr.map(async (item) => {
    return await item.run();
  })
);
```

`reduce()` 函数能够将某个函数作用于数组中的每个元素，从而将多个值转换为单个值；其典型的用法为计算数组和值，或者进行数组扁平化：

```js
// 指定初始值
let result = arr.reduce(callback, initValue);

// 计算数组和值
let sum = arr.reduce((acc, val) => {
  return acc + val;
});

// 使用 reduce 进行数组扁平化
const flatten = (arr) => arr.reduce((a, v) => a.concat(v), []);
// flatten([1,[2],3,4]) -> [1,2,3,4]

// 深度扁平化
const flattenDepth = (arr, depth = 1) =>
  depth != 1
    ? arr.reduce(
        (a, v) => a.concat(Array.isArray(v) ? flattenDepth(v, depth - 1) : v),
        []
      )
    : arr.reduce((a, v) => a.concat(v), []);
// flattenDepth([1,[2],[[[3],4],5]], 2) -> [1,2,[3],4,5]
```

数组元素的排序：

```js
// 反转元素（最前的排到最后、最后的排到最前），返回数组地址
arrayObj.reverse();

// 对数组元素排序，返回数组地址
arrayObj.sort();
```

数组元素的字符串化：

```js
// 返回字符串，这个字符串将数组的每一个元素值连接在一起，中间用 separator 隔开。
arrayObj.join(separator);
```

## Set

```js
// it contains
// ["sumit","amit","anil","anish"]
let set1 = new Set(["sumit", "sumit", "amit", "anil", "anish"]);

// it contains 'f', 'o', 'd'
let set2 = new Set("fooooooood");

// it contains [10, 20, 30, 40]
let set3 = new Set([10, 20, 30, 30, 40, 40]);

set1.add(30).add(40).add(50);

console.log(set1.has(50));

set1.delete("e");

// clearing set2
set2.clear();

// Using Set.prototype.entries()
// creating set
let set1 = new Set();

// adding element to the set
set1.add(50);
set1.add(30);
set1.add(40);
set1.add(20);
set1.add(10);

// using entries to get iterator
let getEntriesArry = set1.entries();

// each iterator is array of [value, value]
// prints [50, 50]
console.log(getEntriesArry.next().value);
```

## Map

Map 对象和 Object 对象的区别如下：

- 一个对象通常都有自己的原型，所以一个对象总有一个"prototype"键
- 一个对象的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值
- 可以通过 size 属性很容易地得到一个 Map 的键值对个数，而对象的键值对个数只能手动确认

## Typed Arrays & Buffer

Typed Arrays 允许我们在 JavaScript 中处理二进制数据与结构，最早是用于 WebGL API 中，以缓解标准 JavaScript 数组转换与类型推测过慢的问题。

```js
// Floating point arrays.
let f64 = new Float64Array(8);
let f32 = new Float32Array(16);

// Signed integer arrays.
// size in bytes: 4
let i32 = new Int32Array(16);
// size in bytes: 2
let i16 = new Int16Array(32);
// size in bytes: 1
let i8 = new Int8Array(64);

// Unsigned integer arrays.
let u32 = new Uint32Array(16);
let u16 = new Uint16Array(32);
let u8 = new Uint8Array(64);
let pixels = new Uint8ClampedArray(64);
```

其典型的场景譬如 WebGL 中获取数据：

```js
gl.bufferData(
  gl.ARRAY_BUFFER,
  new Float32Array(textureCoordinates),
  gl.STATIC_DRAW
);
```

或者获取 Canvas 中的图像数据：

```ks
const uint8ClampedArray = ctx.getImageData(...).data;
```

ArrayBuffer 用于表示通用的、固定长度的二进制数据缓冲，我们并不能直接操作 ArrayBuffer 的内容；而是需要创建新的 Type Arrays 或者 DataView 对象，来获取固定格式的 ArrayBuffer 的值。

```js
// 字节长度为 8
const buffer = new ArrayBuffer(8);

// Int32Array(2) [0, 0]
const view = new Int32Array(buffer);
```

SharedArrayBuffer 类似于 ArrayBuffer，不过其是基于共享内存，因此可以用于进程间通信的场景，譬如 UI 线程与 WebWorker 之间传递数据：

```js
const sab = new SharedArrayBuffer(1024);
worker.postMessage(sab);
```

# 函数

## Definition | 定义

基础的函数定义分为了函数表达式(Function Expression)与函数声明(Function Declaration)，函数表达式并不会被提升到作用域首部，而函数声明则会被提升：

```js
// Function Expression
let sum = function (a, b) {
  return a + b;
};

// Function Declaration
function sum(a, b) {
  return a + b;
}
```

JavaScript 默认不支持函数重载，但是就像 Redux 这样的库可以通过默认参数等方式实现重载的需求：

```js
export default function createStore(reducer, preloadedState, enhancer) {
  if (typeof preloadedState === "function" && typeof enhancer === "undefined") {
    enhancer = preloadedState;
    preloadedState = undefined;
  }
}
```

## 参数

ES6 中引入了所谓的默认参数:

```js
// 传统的默认参数编写方式
function filterEvil(array, evil) {
  evil = evil || "darth vader";
  return array.filter((item) => item !== evil);
}

// ES6 默认参数
function filterEvil(array, evil = "darth vader") {
  return array.filter((item) => item !== evil);
}

// 默认参数可以用来进行必要参数检测
const isRequired = () => {
  throw new Error("param is required");
};

function filterEvil(array, evil = isRequired()) {
  return array.filter((item) => item !== evil);
}
```

## Execution | 执行

可以使用 apply 来连接两个数组：

```js
let countries = ["Moldova", "Ukraine"];
let otherCountries = ["USA", "Japan"];
countries.push.apply(countries, otherCountries);
console.log(countries); // => ['Moldova', 'Ukraine', 'USA', 'Japan']
```

较为全面的 JavaScript 中函数调用方式列举如下：

```js
console.log(1);
(_ => console.log(2))();
eval('console.log(3);');
console.log.call(null, 4);
console.log.apply(null, [5]);
new Function('console.log(6)')();
Reflect.apply(console.log, null, [7])
Reflect.construct(function(){console.log(8)}, []);
Function.prototype.apply.call(console.log, null, [9]);
Function.prototype.call.call(console.log, null, 10);
new (require('vm').Script)('console.log(11)‘).runInThisContext();
```

Throttling will delay executing a function. It will reduce the notifications of an event that fires multiple times.

Debouncing will bunch a series of sequential calls to a function into a single call to that function. It ensures that one notification is made for an event that fires multiple times.

## Generator & Iterator | 生成器与迭代器

生成器是一种返回迭代器的函数，通过 function 关键字后的星号（\*）来表示，函数中会用到新的关键字 yield。在 ES6 中，所有的集合对象（数组、Set 集合及 Map 集合）和字符串都是可迭代对象，可迭代对象都绑定了默认的迭代器。

`yield` 与 `next` 在生成器中扮演者非常重要的角色，前者是操作符，后者则是生成器上的属性函数，二者满足如下特性：

- 生成器的语句会在外部调用 `next` 函数时执行，即我们可以在生成器之外控制其内部操作的执行过程。
- 当生成器执行到 `yield` 操作符时会立即执行 `yield` 之后的语句并且暂停，语句的值作为上一步 `next` 函数的返回值，其是形如 `{done:false, value:x}` 的对象。
- 继续调用 `next` 函数会使生成器继续执行，此处 `next` 函数的参数值会作为整个 `yield` 语句的值；生成器继续执行直到再次遇到 `yield`，或是遇到 `return`/`throw` 生成器就退出。
- `next` 函数的返回值具有三种情况：
  - 如果再次遇到 `yield`，`next` 返回值中的 `value` 属性是紧接在这条 `yield` 之后的语句执行之后的返回值；
  - 如果遇到的是 `return`，那么返回对象 `{done:true, value}` 则是 `return` 的返回值；
  - 其他情况下，返回对象 `{done:false, value:undefined}` ;

我们可以通过简单的例子来验证上述流程描述：

```js
const iter = (function* gen() {
  console.log(`yield ${yield "a" + 0}`);
  console.log(`yield ${yield "b" + 1}`);
  return "c" + 2;
})();

console.log(`next:${iter.next(0).value}`); //输出 next:a0
console.log(`next:${iter.next(1).value}`); //输出 yield 1 next:b1
console.log(`next:${iter.next(2).value}`); //输出 yield 2 next:c2
```

可迭代对象，都有一个 Symbol.iterator 方法，for-of 循环时，通过调用 colors 数组的 Symbol.iterator 方法来获取默认迭代器的，这一过程是在 JavaScript 引擎背后完成的。

```js
let values = [1, 2, 3];
let iterator = values[Symbol.iterator]();

console.log(iterator.next()); // "{ value: 1, done: false}"
console.log(iterator.next()); // "{ value: 2, done: false}"
console.log(iterator.next()); // "{ value: 3, done: false}"
console.log(iterator.next()); // "{ value: undefined, done: true}"
```

# 类与对象

## Object

```js
let object = {
  // `abc` is a valid identifier; no quotes are needed
  abc: 1,
  // `123` is a numeric literal; no quotes are needed
  123: 2,
  // `012` is an octal literal with value `10` and thus isn’t allowed in strict mode; but if you insist on using it, quotes aren’t needed
  012: 3,
  // `π` is a valid identifier; no quotes are needed
  π: Math.PI,
  // `let` is a valid identifier name (although it’s a reserved word); no quotes are needed
  let: 4,
  // `foo bar` is not a valid identifier name; quotes are required
  "foo bar": 5,
  // `foo-bar` is not a valid identifier name; quotes are required
  "foo-bar": 6,
  // the empty string is not a valid identifier name; quotes are required
  "": 7,
};
```

### 对象创建

```js
o = Object.create(Object.prototype, {
  // foo 会成为所创建对象的数据属性
  foo: { writable: true, configurable: true, value: "hello" },
  // bar 会成为所创建对象的访问器属性
  bar: {
    configurable: false,
    get: function () {
      return 10;
    },
    set: function (value) {
      console.log("Setting `o.bar` to", value);
    },
  },
});
```

### 对象拷贝

```js
let o1 = { a: 1 };
let o2 = { b: 2 };
let o3 = { c: 3 };

let obj = Object.assign(o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 }
console.log(o1); // { a: 1, b: 2, c: 3 }, 注意目标对象自身也会改变。
```

> 📖 [JavaScript 异步编程综述]()节选自 [JavaScript CheatSheet | 现代 JavaScript 语法速览与实战清单]()，依次介绍了 JavaScript 异步编程相关的回调、Promise、生成器、async/await 等相关内容。

# 异步编程

异步函数语法在其他语言中存在已久，就像 C# 中的 async/await、Kotlin 中的 coroutines、Go 中的 goroutines；而随着 Node.js 8 的发布，async/await 语法也得到了原生支持而不再需要依赖于 Babel 等转化工具。

## Callback | 回调

## Promise

## 生成器

[tj/co](https://github.com/tj/co)

```js
co(function* () {
  var result = yield Promise.resolve(true);
  return result;
}).then(
  function (value) {
    console.log(value);
  },
  function (err) {
    console.error(err.stack);
  }
);
```

## async/await

```js
class Sleep {
  constructor(timeout) {
    this.timeout = timeout;
  }
  then(resolve, reject) {
    const startTime = Date.now();
    setTimeout(() => resolve(Date.now() - startTime), this.timeout);
  }
}

(async () => {
  const actualTime = await new Sleep(1000);
  console.log(actualTime);
})();
```

```js
const http = require("http");

http
  .createServer(async (req, res) => {
    try {
      let body = "";
      req.setEncoding("utf8");
      for await (const chunk of req) {
        body += chunk;
      }
      res.write(body);
      res.end();
    } catch {
      res.statusCode = 500;
      res.end();
    }
  })
  .listen(1337);
```

# 其他

## ES6 Module | 模块

ES2015 Modules 中主要的关键字就是 `import` 与 `export`，前者负责导入模块而后者负责导出模块。完整的导出语法如下所示：

```js
// default exports
export default 42;
export default {};
export default [];
export default foo;
export default function() {}
export default class {}
export default function foo() {}
export default class foo {}

// letiables exports
export let foo = 1;
export let foo = function() {};
export let bar; // lazy initialization
export let foo = 2;
export let bar; // lazy initialization
export const foo = 3;
export function foo() {}
export class foo {}

// named exports
export { foo };
export { foo, bar };
export { foo as bar };
export { foo as default };
export { foo as default, bar };

// exports from
export * from "foo";
export { foo } from "foo";
export { foo, bar } from "foo";
export { foo as bar } from "foo";
export { foo as default } from "foo";
export { foo as default, bar } from "foo";
export { default } from "foo";
export { default as foo } from "foo";
```

相对应的完整的支持的导入方式如下所示：

```js
// default imports
import foo from "foo";
import {default as foo} from "foo";

// named imports
import {bar} from "foo";
import {bar, baz} from "foo";
import {bar as baz} from "foo";
import {bar as baz, xyz} from "foo";

// glob imports
import * as foo from "foo";

// mixing imports
import foo, {baz as xyz} from "foo";
import * as bar, {baz as xyz} from "foo";
import foo, * as bar, {baz as xyz} from "foo";
```

## Error Handling | 异常处理

```js
try {
  let hello = prompt("Type hello");
  if (hello !== "hello") {
    throw new Error("Oops, you didn't type hello");
  }
} catch (e) {
  alert(e.message);
} finally {
  alert("thanks for playing!");
}
```

# WTF

```
// 0[object Object]1
{} + [] + {} + [1]

// NaN[object Object]
{} + [1,2] + {} + []
```

```js
// false，等式两侧存在 NaN，则为 false
NaN == NaN

// 先进行 Bool 操作转化为 false，然后两侧都变为数字 0
[] == ![]
```
