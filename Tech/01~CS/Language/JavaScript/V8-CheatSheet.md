# V8 CheatSheet | JavaScript V8 引擎必知必会

![image](https://user-images.githubusercontent.com/5803001/45958159-46563300-c049-11e8-8541-9084b5f818ea.png)

# Parse | 语法解析

# Compile | 编译

# GC 垃圾回收

V8 还比较简单，采用分两代的 GC，其中 new space 用 copying GC，然后 global GC 根据碎片化状况选择性使用 mark-sweep 或 mark-compact。

```js
void MarkCompactCollector::CollectGarbage() {
  Prepare();

  MarkLiveObjects();

  SweepLargeObjectSpace();

  if (compacting_collection_) {
    EncodeForwardingAddresses();

    UpdatePointers();

    RelocateObjects();

    RebuildRSets();

  } else {
    SweepSpaces();
  }

  Finish();
}
```

## Concurrent Marking | 并发标记

主流 GC 方案就两种：引用计数和标记清除。引用计数目前已被主流 JavaScript 引擎所抛弃，只有老 IE（<=8）的 JScript 引擎在使用。对象引用关系可以使用一张从根结点（应用程序使用到的全局对象和内建对象）出发的树形图来描述。V8 引擎使用黑白灰三种颜色标记对象的活动状态，黑色表示对象处于活动状态，灰色表示该对象尚未标记完成，白色表示该对象处于未标记状态，可以被 GC 回收。如下图所示，当 GC 开始工作时，会从一些全局的内建对象（Roots）开始标记，可以看到此时除了 Roots 外，其它对象都处于未标记状态：

![image](https://user-images.githubusercontent.com/5803001/45958455-10fe1500-c04a-11e8-8292-070a13c8ed77.png)
