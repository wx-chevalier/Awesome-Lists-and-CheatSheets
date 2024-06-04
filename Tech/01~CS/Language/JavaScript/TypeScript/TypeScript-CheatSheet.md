![1_sso_vplej49wti_ubptvgq](https://user-images.githubusercontent.com/5803001/40587814-0000e1f2-6207-11e8-9e38-2e478a645c31.png)

> 📌 本文侧重于盘点 TypeScript 中类型声明与校验规则相关的知识点，对于与 ECMAScript 语法使用重合的部分建议阅读 [JavaScript CheatSheet](https://parg.co/Yha) 或者 [ECMAScript CheatSheet](https://parg.co/YhW)，对于 TypeScript 在 React/Redux 中的实践可以参阅 [React CheatSheet/TypeScript]()。需要声明的是，本文参考了 [TypeScript Links]() 中列举的很多文章或书籍，特别是官方的 [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/basic-types.html) 很值得仔细阅读。

# TypeScript CheatSheet | TypeScript 语法实践速览与实践清单

TypeScript 是由 MicroSoft 出品的 JavaScript 超集，它在兼容 JavaScript 的所有特性的基础上，附带了静态类型的支持；TypeScript 还允许我们使用尚未正式发布的 ECMAScript 的语言特性，在编译时进行类似于 Babel 这样的降级转化。

JavaScript 本身乃动态类型的语言，即是在运行时才进行类型校验；该特性赋予了其快速原型化的能力，却在构建大型 JavaScript 应用时力有不逮，其无法在编译时帮助规避可能的类型错误，也无法利用自动补全、自动重构等工具特性。TypeScript 的静态类型特性则帮助我们在编译时尽可能规避类型错误，并且 TypeScript 会尽可能地从上下文信息中进行类型推导，以避免像 Java 等静态类型语言中过于冗余的麻烦。

对于 TypeScript 的语法速览可以参考本目录下的 [ts-snippets](https://parg.co/QNv)。

## 快速开始

可以参考 [`fe-boilerplate/*-ts`]() 或者 [`Backend-Boilerplate/node`]()，如果想了解 TypeScript 在 React 中的应用，可以参考 [React CheatSheet/TypeScript 节]()。们可以通过 npm 安装 TypeScript 的依赖包：

```sh
# 全局安装
$ npm install -g typescript

# 检测是否安装成功
$ tsc -v
Version 2.8.3
```

TypeScript 源文件一般使用 `.ts` 或者 `.tsx` 为后缀，其并不能直接运行在浏览器中而需要进行编译转化，TypeScript 的官方提供了 `tsc` 命令来进行文件编译：

```sh
$ tsc main.ts

# 同时编译多个文件
$ tsc main.ts worker.ts

# 编译当前目录下的全部 ts 文件，并不会递归编译
$ tsc *.ts

# 启动后台常驻编译程序
$ tsc main.ts --watch
```

在实际的项目中，我们也往往会在项目根目录配置 tsconfig.json 文件，来个性化配置 TypeScript 的编译参数：

```json
{
  "compilerOptions": {
    "outDir": "./dist/es",
    "declarationDir": "./dist/types",
    "target": "es5",
    "module": "commonjs",
    "jsx": "react",
    "downlevelIteration": true,
    "moduleResolution": "node",
    "allowUnreachableCode": true,
    "declaration": true,
    "experimentalDecorators": true,
    "noImplicitAny": true,
    "noImplicitReturns": true,
    "noImplicitThis": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "pretty": true,
    "skipLibCheck": true,
    "sourceMap": true,
    "strictNullChecks": true,
    "suppressImplicitAnyIndexErrors": true,
    "lib": ["dom", "es2015"],
    "baseUrl": "src"
  },
  "include": ["src/**/*", "typings/**/*"]
}
```

也可以使用 [ts-node](https://github.com/TypeStrong/ts-node) 快速地直接运行 TypeScript 文件；

# 常用内建类型

## Partial<Type>

构建一个类型的所有属性都设置为可选的类型：

```ts
// 实现
type Partial<T> = {
  [P in keyof T]?: T[P];
};

interface NodeConfig {
  appName: string;
  port: number;
}

class NodeAppBuilder {
  private configuration: NodeConfig = {
    appName: "NodeApp",
    port: 3000,
  };

  private updateConfig<Key extends keyof NodeConfig>(
    key: Key,
    value: NodeConfig[Key]
  ) {
    this.configuration[key] = value;
  }

  config(config: Partial<NodeConfig>) {
    type NodeConfigKey = keyof NodeConfig;

    for (const key of Object.keys(config) as NodeConfigKey[]) {
      const updateValue = config[key];

      if (updateValue === undefined) {
        continue;
      }

      this.updateConfig(key, updateValue);
    }

    return this;
  }
}

// `Partial<NodeConfig>`` allows us to provide only a part of the
// NodeConfig interface.
new NodeAppBuilder().config({ appName: "ToDoApp" });
```

keyof 可以取得一个对象接口所有的 key，in 遍历枚举类型,后面的内容都会用到：

```js
type T = keyof Todo ->  // "title" | "description"

type Obj = {
 [p in Todo] : Todo[p]   //  title: string; description: string;
}
```

## Required<Type>

构建一个类型的所有可选的属性都设置为比必填的类型，与 Partial 相反：

```js
type Required<T> = {
    [P in keyof T]-?: T[P];
};

interface ContactForm {
 		email?: string;
 		message?: string;
 }

 function submitContactForm(formData: Required<ContactForm>) {
 		// Send the form data to the server.
 }

 submitContactForm({
 		email: 'ex@mple.com',
 		message: 'Hi! Could you tell me more about…',
 });

 // TypeScript error: missing property 'message'
 submitContactForm({
 		email: 'ex@mple.com',
 });
```

上文对应的 -？代表着去掉可选，与之对应的还有 +？，两者正好相反。

## Readonly<Type>

将所有的属性设为只读：

```js
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};

enum LogLevel {
 		Off,
 		Debug,
 		Error,
 		Fatal
 };

 interface LoggerConfig {
 		name: string;
 		level: LogLevel;
 }

 class Logger {
 		config: Readonly<LoggerConfig>;

 		constructor({name, level}: LoggerConfig) {
 				this.config = {name, level};
 				Object.freeze(this.config);
 		}
 }

 const config: LoggerConfig = {
 	name: 'MyApp',
 	level: LogLevel.Debug
 };

 const logger = new Logger(config);

 // TypeScript Error: cannot assign to read-only property.
 logger.config.level = LogLevel.Error;

 // We are able to edit config variable as we please.
 config.level = LogLevel.Error;
```

## Record<Keys,Type>

Keys 变成 keys，Type 变成 values：

```js
type Record<K extends keyof any, T> = {
    [P in K]: T;
};

// Positions of employees in our company.
 type MemberPosition = 'intern' | 'developer' | 'tech-lead';

 // Interface describing properties of a single employee.
 interface Employee {
 		firstName: string;
 		lastName: string;
 		yearsOfExperience: number;
 }

 // Create an object that has all possible `MemberPosition` values set as keys.
 // Those keys will store a collection of Employees of the same position.
 const team: Record<MemberPosition, Employee[]> = {
 		intern: [],
 		developer: [],
 		'tech-lead': [],
 };

 // Our team has decided to help John with his dream of becoming Software Developer.
 team.intern.push({
 	firstName: 'John',
 	lastName: 'Doe',
 	yearsOfExperience: 0
 });

 // `Record` forces you to initialize all of the property keys.
 // TypeScript Error: "tech-lead" property is missing
 const teamEmpty: Record<MemberPosition, null> = {
 		intern: null,
 		developer: null,
 };
```

## Pick<Type, Keys>

从 Type 选择一组 Keys 属性：

```js
type Pick<T, K extends keyof T> = {
    [P in K]: T[P];
};
// K extends keyof T,这句表示，确保K是T的子集

interface Article {
 		title: string;
 		thumbnail: string;
 		content: string;
 }

 // Creates new type out of the `Article` interface composed
 // from the Articles' two properties: `title` and `thumbnail`.
 // `ArticlePreview = {title: string; thumbnail: string}`
 type ArticlePreview = Pick<Article, 'title' | 'thumbnail'>;

 // Render a list of articles using only title and description.
 function renderArticlePreviews(previews: ArticlePreview[]): HTMLElement {
 		const articles = document.createElement('div');

 		for (const preview of previews) {
 				// Append preview to the articles.
 		}

 		return articles;
 }

 const articles = renderArticlePreviews([
 		{
 			title: 'TypeScript tutorial!',
 			thumbnail: '/assets/ts.jpg'
 		}
 ]);
```

## Omit<Type, Keys>

从 Type 选择所有属性，然后在删除 Keys：

```js
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;

interface Animal {
 		imageUrl: string;
 		species: string;
 		images: string[];
 		paragraphs: string[];
 }

 // Creates new type with all properties of the `Animal` interface
 // except 'images' and 'paragraphs' properties. We can use this
 // type to render small hover tooltip for a wiki entry list.
 type AnimalShortInfo = Omit<Animal, 'images' | 'paragraphs'>;

 function renderAnimalHoverInfo (animals: AnimalShortInfo[]): HTMLElement {
 		const container =  document.createElement('div');
 		// Internal implementation.
 		return container;
 }
```

## Exclude<Type, ExcludedUnion>

通过从 Type 中排除可分配给 ExcludedUnion 的所有联合成员来构造类型，类似于差集：

```js
type Exclude<T, U> = T extends U ? never : T;

type Todo:Exclude<"a" | "b" | "c", "a">
//  type Todo = "b" | "c"

interface ServerConfig {
 	port: null | string | number;
 }

 type RequestHandler = (request: Request, response: Response) => void;

 // Exclude `null` type from `null | string | number`.
 // In case the port is equal to `null`, we will use default value.
 function getPortValue(port: Exclude<ServerConfig['port'], null>): number {
 	if (typeof port === 'string') {
 		return parseInt(port, 10);
 	}

 	return port;
 }

 function startServer(handler: RequestHandler, config: ServerConfig): void {
 	const server = require('http').createServer(handler);

 	const port = config.port === null ? 3000 : getPortValue(config.port);
 	server.listen(port);
 }
```

## Extract<Type, Union>

通过从 Type 中提取可分配 Union 的所有联合成员来构造类型，类似于交集：

```js
type Exclude<T, U> = T extends U ? T : never;

type Todo:Exclude<"a" | "b" | "c", "a"> = { 'a' }

declare function uniqueId(): number;

 const ID = Symbol('ID');

 interface Person {
 	[ID]: number;
 	name: string;
 	age: number;
 }

 // Allows changing the person data as long as the property key is of string type.
 function changePersonData<
 	Obj extends Person,
 	Key extends Extract<keyof Person, string>,
 	Value extends Obj[Key]
 > (obj: Obj, key: Key, value: Value): void {
 	obj[key] = value;
 }

 // Tiny Andrew was born.
 const andrew = {
 	[ID]: uniqueId(),
 	name: 'Andrew',
 	age: 0,
 };

 // Cool, we're fine with that.
 changePersonData(andrew, 'name', 'Pony');

 // Goverment didn't like the fact that you wanted to change your identity.
 changePersonData(andrew, ID, uniqueId());
```

## NonNullable

通过从 Type 中排除 null 和 undefined 来构造类型：

```ts
type NonNullable<T> = T extends null | undefined ? never : T;

const A: NonNullable<string | boolean | null | undefined>;
// A只能是string或者boolean，不能是null或undefined

type PortNumber = string | number | null;

/** Part of a class definition that is used to build a server */
class ServerBuilder {
  portNumber!: NonNullable<PortNumber>;

  port(this: ServerBuilder, port: PortNumber): ServerBuilder {
    if (port == null) {
      this.portNumber = 8000;
    } else {
      this.portNumber = port;
    }

    return this;
  }
}

const serverBuilder = new ServerBuilder();

serverBuilder
  .port("8000") // portNumber = '8000'
  .port(null) // portNumber =  8000
  .port(3000); // portNumber =  3000

// TypeScript error
serverBuilder.portNumber = null;
```

## Parameters

从函数类型 type 的形参中使用的类型构造元组类型：

```ts
type Parameters<T extends (...args: any) => any> = T extends (
  ...args: infer P
) => any
  ? P
  : never;

type A = Parameters<(s: string) => void>;
const obj: A = ["11"];

type B = Parameters<<T>(arg: T) => T>;
const obj1: B = [1]; // 任意类型都可以

type C = Parameters<string>;
// 类型“string”不满足约束“(...args: any) => any”

/** Obtain the parameters of a function type in a tuple. */
function shuffle(input: any[]): void {
  // Mutate array randomly changing its' elements indexes.
}

function callNTimes<Fn extends (...args: any[]) => any>(
  func: Fn,
  callCount: number
) {
  // Type that represents the type of the received function parameters.
  type FunctionParameters = Parameters<Fn>;

  return function (...args: FunctionParameters) {
    for (let i = 0; i < callCount; i++) {
      func(...args);
    }
  };
}

const shuffleTwice = callNTimes(shuffle, 2);
```

## ConstructorParameters

在一个元组中获得一个构造函数类型的参数。

```ts
class ArticleModel {
  title: string;
  content?: string;

  constructor(title: string) {
    this.title = title;
  }
}

class InstanceCache<T extends new (...args: any[]) => any> {
  private ClassConstructor: T;
  private cache: Map<string, InstanceType<T>> = new Map();

  constructor(ctr: T) {
    this.ClassConstructor = ctr;
  }

  getInstance(...args: ConstructorParameters<T>): InstanceType<T> {
    const hash = this.calculateArgumentsHash(...args);

    const existingInstance = this.cache.get(hash);
    if (existingInstance !== undefined) {
      return existingInstance;
    }

    return new this.ClassConstructor(...args);
  }

  private calculateArgumentsHash(...args: any[]): string {
    // Calculate hash.
    return "hash";
  }
}

const articleCache = new InstanceCache(ArticleModel);
const amazonArticle = articleCache.getInstance("Amazon forests burining!");
```

## ReturnType<T>

获得一个函数类型的返回类型。

```js
/** Provides every element of the iterable `iter` into the `callback` function and stores the results in an array. */
 function mapIter<
 		Elem,
 		Func extends (elem: Elem) => any,
 		Ret extends ReturnType<Func>
 >(iter: Iterable<Elem>, callback: Func): Ret[] {
 		const mapped: Ret[] = [];

 		for (const elem of iter) {
 				mapped.push(callback(elem));
 		}

 		return mapped;
 }

 const setObject: Set<string> = new Set();
 const mapObject: Map<number, string> = new Map();

 mapIter(setObject, (value: string) => value.indexOf('Foo')); // number[]

 mapIter(mapObject, ([key, value]: [number, string]) => {
 		return key % 2 === 0 ? value : 'Odd';
 }); // string[]
```

## InstanceType<T>

获取一个构造函数类型的实例类型。

```js
class IdleService {
 		doNothing (): void {}
 }

 class News {
 		title: string;
 		content: string;

 		constructor(title: string, content: string) {
 				this.title = title;
 				this.content = content;
 		}
 }

 const instanceCounter: Map<Function, number> = new Map();

 interface Constructor {
 		new(...args: any[]): any;
 }

 // Keep track how many instances of `Constr` constructor have been created.
 function getInstance<
 		Constr extends Constructor,
 		Args extends ConstructorParameters<Constr>
 >(constructor: Constr, ...args: Args): InstanceType<Constr> {
 		let count = instanceCounter.get(constructor) || 0;

 		const instance = new constructor(...args);

 		instanceCounter.set(constructor, count + 1);

 		console.log(`Created ${count + 1} instances of ${Constr.name} class`);

 		return instance;
 }


 const idleService = getInstance(IdleService);
 // Will log: `Created 1 instances of IdleService class`
 const newsEntry = getInstance(News, 'New ECMAScript proposals!', 'Last month...');
 // Will log: `Created 1 instances of News class`
```

## Uppercase<S extends string>

将字符串中的每个字符都转为大写字母。

```ts
type T = Uppercase<"hello">; // 'HELLO'

type T2 = Uppercase<"foo" | "bar">; // 'FOO' | 'BAR'

type T3<S extends string> = Uppercase<`aB${S}`>;
type T4 = T30<"xYz">; // 'ABXYZ'

type T5 = Uppercase<string>; // string
type T6 = Uppercase<any>; // any
type T7 = Uppercase<never>; // never
type T8 = Uppercase<42>; // Error, type 'number' does not satisfy the constraint 'string'
```

## Lowercase<S extends string>

将字符串中的每个字符都转为小写。

```ts
type T = Lowercase<"HELLO">; // 'hello'

type T2 = Lowercase<"FOO" | "BAR">; // 'foo' | 'bar'

type T3<S extends string> = Lowercase<`aB${S}`>;
type T4 = T32<"xYz">; // 'abxyz'

type T5 = Lowercase<string>; // string
type T6 = Lowercase<any>; // any
type T7 = Lowercase<never>; // never
type T8 = Lowercase<42>; // Error, type 'number' does not satisfy the constraint 'string'
```

## Capitalize<S extends string>

将一个字符串中的第一个字符转换成大写字母。

```ts
type T = Capitalize<"hello">; // 'Hello'

type T2 = Capitalize<"foo" | "bar">; // 'Foo' | 'Bar'

type T3<S extends string> = Capitalize<`aB${S}`>;
type T4 = T32<"xYz">; // 'ABxYz'

type T5 = Capitalize<string>; // string
type T6 = Capitalize<any>; // any
type T7 = Capitalize<never>; // never
type T8 = Capitalize<42>; // Error, type 'number' does not satisfy the constraint 'string'
```

## Uncapitalize<S extends string>

将字符串中的第一个字符转为小写。

```ts
type T = Uncapitalize<"Hello">; // 'hello'

type T2 = Uncapitalize<"Foo" | "Bar">; // 'foo' | 'bar'

type T3<S extends string> = Uncapitalize<`AB${S}`>;
type T4 = T30<"xYz">; // 'aBxYz'

type T5 = Uncapitalize<string>; // string
type T6 = Uncapitalize<any>; // any
type T7 = Uncapitalize<never>; // never
type T8 = Uncapitalize<42>; // Error, type 'number' does not satisfy the constraint 'string'
```
