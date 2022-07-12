# 组合模式

**定义：** 将对象组合成树形结构以表示“部分-整体”的层次结构。组合模式使得用户对单个对象和组合对象的使用具有一致性

**类型：** 结构型

**类图：** 

![image-20210522105838736](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/DesignPattern/Composite.png)

**组件说明：**

- Component：组合中的对象声明接口，在适当情况下实现所有类共有接口的默认行为。声明了一个接口用于访问和管理Component

  的子部件

- Leaf：在组合中表示叶节点对象，叶节点没有子节点

- Composite ：定义枝节点行为，用来存储子部件，在Component接口中实现与子部件有关的操作，比如增加和删除

**适用场景：** 

- 部分整体场景，如树形菜单，文件、文件夹的管理

**应用实例：** 算术表达式包括操作数、操作符和另一个操作数，其中，另一个操作符也可以是操作数、操作符和另一个操作数

**优点：** 

- 高层模块调用简单
- 节点自由增加

**缺点：** 

- 在使用组合模式时，其叶子和树枝的声明都是实现类，而不是接口，违反了依赖倒置原则。