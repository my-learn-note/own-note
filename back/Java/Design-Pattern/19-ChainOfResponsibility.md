# 职责链模式(Chain of Responsibility)

**定义：** 使多个对象都有机会处理请求，从而避免请求的发送者和接受者之间的耦合关系。将这个对象连成一条链，并沿着这条链传递该

请求，这样系统的更改可以在不影响客户端的情况下动态地重新组织和分配责任

**类型：** 行为型

**类图：** 

![image-20210524231308188](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/DesignPattern/ChainOfResponsibility.jpg)

**组件说明：** 

- Handler：定义一个处理请示的接口

- ConcreteHandler：具体处理类，处理它所负责的请求，可访问它的后继者，如果可处理该请求，就处理之，否则就将该请求转发

  给它的后继者

**适用场景：** 

- 有多个对象可以处理同一个请求，具体哪个对象处理该请求由运行时刻自动确定
- 在不明确指定接收者的情况下，向多个对象中的一个提交一个请求
- 可动态指定一组对象处理请求。

**优点：** 

- 降低耦合度。它将请求的发送者和接收者解耦
- 简化了对象。使得对象不需要知道链的结构
- 增强给对象指派职责的灵活性。通过改变链内的成员或者调动它们的次序，允许动态地新增或者删除责任
- 增加新的请求处理类很方便
- 它们仅需一个指向后继者的引用，而不需要保持它所有的候选接受者的引用

**缺点：** 

- 不能保证请求一定被接收
- 系统性能将受到一定影响，而且在进行代码调试时不太方便，可能会造成循环调用
- 可能不容易观察运行时的特征，有碍于除错。