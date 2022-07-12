# 建造者模式

**定义：** 将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示

**类型：** 创建型

**类图：**

![image-20210512141240045](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/DesignPatter/Builder.png)

**组件说明：** 

- Builder：为创建一个Product对象的各个部件指定的抽象接口
- ConcreteBuilder：具体建造者，实现Builer接口，构造和装配各个部件
- Product：具体产品
- Director：指挥者，是构建一个使用Builer接口的对象

**适用场景：**

- 需要生成的对象具有复杂的内部结构
- 需要生成的对象内部属性本身相互依赖

**优点：**

- 建造者独立，易扩展
- 便于控制细节风险

**缺点：**

- 产品必须有共同点，范围有限制
- 需要生成的对象内部属性本身相互依赖