# Gradle CheatSheet

在 Grade 中，我们常见的几个关键术语有 Project、Plugin 以及 Task。和 Maven 一样，Gradle 只是提供了构建项目的一个框架，真正起作用的是 Plugin。Gradle 在默认情况下为我们提供了许多常用的 Plugin，其中包括有构建 Java 项目的 Plugin，还有 War，Ear 等。与 Maven 不同的是，Gradle 不提供内建的项目生命周期管理，只是 Java Plugin 向 Project 中添加了许多 Task，这些 Task 依次执行，为我们营造了一种如同 Maven 般项目构建周期。换言之，Project 为 Task 提供了执行上下文，所有的 Plugin 要么向 Project 中添加用于配置的 Property，要么向 Project 中添加不同的 Task。一个 Task 表示一个逻辑上较为独立的执行过程，比如编译 Java 源代码，拷贝文件，打包 Jar 文件，甚至可以是执行一个系统命令或者调用 Ant。另外，一个 Task 可以读取和设置 Project 的 Property 以完成特定的操作。

# Configuration | 构建配置

## artifacts

和 Maven 一样，Gradle 也是通过 artifact 来打包构建的。得益于上述的 Gradle 本身的特性，artifact 在 Gradle 里实现得更灵活一些。看一个例子：

```groovy
// jar类型的artifact
task myJar(type: Jar)
artifacts {
    archives myJar
}

// file类型的artifact
def someFile = file('build/somefile.txt')
artifacts {
    archives someFile
}

// 根据自定义task来完成artifact
task myTask(type:  MyTaskType) {
    destFile = file('build/somefile.txt')
}
artifacts {
    archives(myTask.destFile) {
        name 'my-artifact'
        type 'text'
        builtBy myTask
    }
}

// 根据自定义task来完成artifact
task generate(type:  MyTaskType) {
    destFile = file('build/somefile.txt')
}
artifacts {
    archives file: generate.destFile, name: 'my-artifact', type: 'text', builtBy: generate
}
```

## publish | 发布

Gradle 构建的项目，发布到仓库中，也非常容易：

```groovy
apply plugin: 'maven'

uploadArchives {
    repositories {
        ivy {
            credentials {
                username "username"
                password "pw"
            }
            url "http://repo.mycompany.com"
        }
    }
}
```

## Properties | 属性

在默认情况下，Gradle 已经为 Project 添加了很多 Property，我们可以调用以下命令进行查看：

```
gradle properties
```

输出如下：

```groovy
:properties

------------------------------------------------------------
Root project
------------------------------------------------------------

allprojects: [root project 'gradle-blog']
ant: org.gradle.api.internal.project.DefaultAntBuilder@1342097

buildDir: /home/davenkin/Desktop/gradle-blog/build
buildFile: /home/davenkin/Desktop/gradle-blog/build.gradle
...
configurations: []
convention: org.gradle.api.internal.plugins.DefaultConvention@11492ed
copyFile: task ':copyFile'
...
ext: org.gradle.api.internal.plugins.DefaultExtraPropertiesExtension@1b5d53a
extensions: org.gradle.api.internal.plugins.DefaultConvention@11492ed
...
helloWorld: task ':helloWorld'
...
plugins: [org.gradle.api.plugins.HelpTasksPlugin@7359f7]
project: root project 'gradle-blog'
...
properties: {...}
repositories: []

tasks: [task ':copyFile', task ':helloWorld']
version: unspecified

BUILD SUCCESSFUL

Total time: 2.667 secs
```

| Name          | Type                                                                                   | Default Value                              |
| ------------- | -------------------------------------------------------------------------------------- | ------------------------------------------ |
| `project`     | [`Project`](https://docs.gradle.org/current/dsl/org.gradle.api.Project.html)           | The `Project` instance                     |
| `name`        | `String`                                                                               | The name of the project directory.         |
| `path`        | `String`                                                                               | The absolute path of the project.          |
| `description` | `String`                                                                               | A description for the project.             |
| `projectDir`  | `File`                                                                                 | The directory containing the build script. |
| `buildDir`    | `File`                                                                                 | `*projectDir*/build`                       |
| `group`       | `Object`                                                                               | `unspecified`                              |
| `version`     | `Object`                                                                               | `unspecified`                              |
| `ant`         | [`AntBuilder`](https://docs.gradle.org/current/javadoc/org/gradle/api/AntBuilder.html) | An `AntBuilder` instance                   |

## Variables | 变量

# Dependence | 依赖管理

```sh
$ gradle dependencies
```

## Repository | 仓库配置

```groovy
repositories {
    mavenCentral()          // 定义仓库为maven中心仓库
}
repositories {
    jcenter()               // 定义仓库为jcenter仓库
}
repositories {
    maven {
        url "http://repo.mycompany.com/maven2"      // 定义依赖包协议是maven，地址是公司的仓库地址
    }
}
repositories {                              // 定义本地仓库目录
    flatDir {
        dirs 'lib'
    }
}
repositories {                              // 定义ivy协议类型的仓库
    ivy {
        url "http://repo.mycompany.com/repo"
    }
}
```

```groovy
repositories {
 mavenCentral artifactUrls:["file://C:/maven/.m2/repository/"]
}
```

如果是系统的默认配置的：

```groovy
repositories {
  mavenLocal()
}
```

## 依赖声明

```groovy
// Now we can set the dependencies by configuring the dependencies closure
// where compile is a configuration not a method that compiles the dependency or so
// It puts the dependency in the classpath of the Java Application
// <groupId>:<artifactId>:<version>
dependencies {
  compile "org.apache.commons:commons-lang3:3.3.2"
}

// Or
dependencies {
  compile group: "org.apache.commons", name: "commons-lang3", version: "3.3.2"
}
```

# Task | 任务

## 检索

Gradle 在默认情况下为我们提供了几个常用的 Task，比如查看 Project 的 Properties、显示当前 Project 中定义的所有 Task 等。可以通过一下命令查看 Project 中所有的 Task：

```sh
$ gradle tasks
```

输出如下：

```groovy
:tasks

------------------------------------------------------------
All tasks runnable from root project
------------------------------------------------------------

Build Setup tasks
-----------------
setupBuild - Initializes a new Gradle build. [incubating]
wrapper - Generates Gradle wrapper files. [incubating]

Help tasks
----------
dependencies - Displays all dependencies declared in root project 'gradle-blog'.
dependencyInsight - Displays the insight into a specific dependency in root project 'gradle-blog'.
help - Displays a help message
projects - Displays the sub-projects of root project 'gradle-blog'.
properties - Displays the properties of root project 'gradle-blog'.
tasks - Displays the tasks runnable from root project 'gradle-blog'.

Other tasks
-----------
copyFile
helloWorld

To see all tasks and more detail, run with --all.

BUILD SUCCESSFUL

Total time: 2.845 secs
```

上面的 other tasks 中列举出来的 task 即是我们自定义的 tasks。

## 定义

Gradle 的 Project 从本质上说只是含有多个 Task 的容器，一个 Task 与 Ant 的 Target 相似，表示一个逻辑上的执行单元。我们可以通过很多种方式定义 Task，所有的 Task 都存放在 Project 的 TaskContainer 中。让我们来看一个最简单的 Task，创建一个 build.gradle 文件，内容如下：

```groovy
// 简略定义
task helloWorld << {
   println "Hello World!"
}

// 上述代码中使用了 `<<` 符号用来表征 `{}` 声明的动作是追加在某个任务的末尾，如果使用全声明即是
task printVersion {
// 任务的初始声明可以添加first和last动作
    doFirst {
        println "Before reading the project version"
    }

    doLast {
        println "Version: $version"
    }
}
```

这里的 `<<` 表示向 helloWorld 中加入执行代码——其实就是 groovy 代码。Gradle 向我们提供了一整套 DSL，所以在很多时候我们写的代码似乎已经脱离了 groovy，但是在底层依然是执行的 groovy。比如上面的 task 关键字，其实就是一个 groovy 中的方法，而大括号之间的内容则表示传递给 task()方法的一个闭包。除了 `<<` 之外，我们还很多种方式可以定义一个 Task。

```groovy
task(hello) << {
    println "hello"
}

task(copy, type: Copy) {
    from(file('srcDir'))
    into(buildDir)
}

//也可以用字符串作为任务名
task('hello') <<
{
    println "hello"
}

task('copy', type: Copy) {
    from(file('srcDir'))
    into(buildDir)
}

//Defining tasks with alternative syntax

tasks.create(name: 'hello') << {
    println "hello"
}

tasks.create(name: 'copy', type: Copy) {
    from(file('srcDir'))
    into(buildDir)
}
```

## Default tasks | 默认任务

Gradle 允许在脚本中配置默认的一到多个任务来响应没有带参数的`gradle`命令：

```groovy
defaultTasks 'clean', 'run'

task clean << {
    println 'Default Cleaning!'
}

task run << {
    println 'Default Running!'
}

task other << {
    println "I'm not a default task!"
}
```

`gradle -q` 命令的输出：

```groovy
> gradle -q
Default Cleaning!
Default Running!
```

# Java Plugin

1，使用 Java plugin，只需要在 build.gradle 中加入这句话：

```groovy
apply plugin: 'java'
```

2，了解或设置 Java project 布局。Gradle 和 Maven 一样，采用了“约定优于配置”的方式对 Java project 布局，并且布局方式是和 Maven 一样的，此外，Gradle 还可以方便的自定义布局。在 Gradle 中，一般把这些目录叫做 source set。看下官方的答案：

![gradle source set](http://tech.meituan.com/img/gradle/source_set.png)

这里要注意，每个 plugin 的 source set 可能都不一样。同样的，Java plugin 还定义好了一堆 task，让我们可以直接使用，比如：clean、test、build 等等。这些 task 都是围绕着 Java plugin 的构建生命周期的：

![](http://tech.meituan.com/img/gradle/javaPluginTasks.png)

图中每一块都是一个 task，箭头表示 task 执行顺序/依赖，比如执行 task jar，那么必须先执行 task compileJava 和 task processResources。另外可以看到，Gradle 的 Java plugin 构建生命周期比较复杂，但是也表明了更加灵活，而且，在项目中，一般只使用其中常用的几个：clean test check build 等等。

gradle 构建过程中，所有的依赖都表现为配置，比如说系统运行时的依赖是 runtime，gradle 里有一个依赖配置叫 runtime，那么系统运行时会加载这个依赖配置以及它的相关依赖。这里说的有点绕，可以简单理解依赖和 maven 类似，只不过 gradle 用 configuration 实现，所以更灵活，有更多选择。下图是依赖配置关系图以及和 task 调用的关系图：

![javaPluginConfigurations](http://tech.meituan.com/img/gradle/javaPluginConfigurations.png)

可以看到，基本和 Maven 是一样的。其实 Gradle 里面这些依赖(scope)都是通过 configuration 来实现的，这里就不细说，有兴趣的可以研究一下官方资料。

## 源码配置

```groovy
// A Closure that configures the sourceSets Task
// Sets the main folder as Source folder (where the compiler is looking up the .java files)
sourceSets {
  main.java.srcDir "src/main"
}

// This can also be written as a function -> srcDir is a method (Syntax sugar of the Groovy language)
souceSets {
  main.java.srcDir("src/main")
}

// Or
sourceSets.main.java.srcDir "src/main"

// Or
sourceSets {
  main {
    java {
      srcDir "src/main"
    }
  }
}

// Or setting the variable directly as a typical groovy enumerational style
sourceSets {
  main.java.srcDirs = ["src/main"]
}
```

## 任务

```sh
# 执行编译，将 Java 源码编译到 build 目录并且打包到 jar 包中
$ gradle build
```

自定义 jar 命令的配置参数:

```groovy
// Configure the jar task to insert the Main Class to the resulting MANIFEST.MF
jar {
  manifest.attributes("Main-Class", "de.example.main.Application")
}

// Or without the parentheses
jar {
  manifest.attributes "Main-Class": "de.example.main.Application"
}

jar {
  from configurations.compile.collect {
    entry -> zipTree(entry)
  }
}

// Or with syntactic sugar
jar {
  from configurations.compile.collect {
    entry -> zipTree entry
  }
}

// And with more syntactic sugar
// (where "it" is like "this" in gradle and "this" is the entry iterating over by the for loop)
jar {
  from configurations.compile.collect {
    zipTree it
  }
}
```

# Web Application

# 测试 | Test
