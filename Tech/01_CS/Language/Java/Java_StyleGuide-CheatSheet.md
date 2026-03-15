# Java StyleGuide CheatSheet | Java 样式指南

当我们敲下每个点号时，都应该考虑：

- 是否会出现空指针？
- 是否会抛出异常？
- 是否在热点区域运行？
- 在哪个线程中执行？
- 是否存在并发锁间隙？
- 是否会并发修改不可见？

```java
// Bad, doesn't compile
switch (value) {
    case 1: int j = 1; break;
    case 2: int j = 2; break;
}

// Good
switch (value) {
    case 1: {
        final int j = 1;
        break;
    }
    case 2: {
        final int j = 2;
        break;
    }

    // Remember:
    default:
        throw new ThreadDeath("That'll teach them");
}
```

Within the switch statement, there is only one scope defined among all the case statements. In fact, these case statements aren’t even really statements, they’re like labels and the switch is a goto call. This means that the variable final int j is defined for all the different cases, regardless if we issue a break or not. Not very intuitive. Which is why it’s always a good idea to create a new, nested scope per case statement via a simple block.

# Java 安全编码索引

信息保护

# 序列化

对于序列化对象而言，应该使用 transient 来定义敏感数据，即避免其被序列化；而使用 serialPersistentFields 定义非敏感数据。

而我们常见的 FileNotFoundException、SQLException、BindException、OutOfMemoryError 等都有可能会引起信息泄露从而给攻击者攻击系统提供帮助。

程序中我们可以使用 SecurityManager、AccessController 来检查代码对于敏感资源或操作的访问权限。

任何敏感情况下都禁用 java.util.Random() 类生成业务的随机数，譬如 Web 应用会话标识、验证码随机数、安全敏感文件的随机文件名、生成密钥相关的随机数。

内存安全

校验过滤

线程安全
