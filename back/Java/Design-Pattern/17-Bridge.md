# 桥接模式(Bridge)

**定义：** 将抽象部分和它的实现部分分离，使它们都可以独立地变化。抽象和实现分离并不是指让抽象类与其派生类分离，这样就没有

任何意义。实现指的是抽象类和它的派生类用来实现自己的对象

**类型：** 结构型

**类图：** ![image-20210523204346027](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/DesignPattern/Bridge.jpg)

**组件说明：** 

- Abstraction：抽象
- RefinedAbstraction：被提炼的抽象
- Implementor：实现
- ConcreteImplementor：具体实现

**适用场景：** 

- 如果一个系统需要在构件的抽象化角色和具体化角色之间增加更多的灵活性，避免在两个层次之间建立静态的继承联系，通过桥接模

  式可以使它们在抽象层建立一个关联关系

- 对于那些不希望使用继承或因为多层次继承导致系统类的个数急剧增加的系统，桥接模式尤为适用

- 一个类存在两个独立变化的维度，且这两个维度都需要进行扩展。

**优点：** 

- 抽象和实现的分离
- 优秀的扩展能力
- 实现细节对客户透明

**缺点：** 

- 桥接模式的引入会增加系统的理解与设计难度，由于聚合关联关系建立在抽象层，要求开发者针对抽象进行设计与编程。