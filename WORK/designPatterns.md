## 工厂模式

### 简单工厂

一个工厂根据输入创建出多种对象

在业务较简单，工厂类不会经常更改的情况

若有修改，修改工厂

违反开闭原则

### 工厂模式

每个派生工厂创建出一种对象

每种派生对象需要一个工厂，代码太多

### 抽象工厂模式

每个派生工厂创建出多种对象（属于一个产品族）

## 设计模式

用设计模式不一定是好事，不用设计模式不一定是坏事

我认为那本书的精华之所在是开头介绍的几大原则，开闭原则，单一职责原则，依赖倒置，接口分离，里氏替换。。。记不全了，还有什么对其他对象所知尽量少

至于那23种设计模式，只是给大家打个样儿，告诉大家如何贯彻前面的原则

设计模式真正学通的样子，应该是“无招胜有招”，“运用之妙，存乎一心”，“随心所欲，不逾矩”，能够面对具体的新问题，自然而然地用那些原则思考、设计和实现，看似大张大合、天马行空，仔细检查却一点也不“犯规”，功能、性能、维护性都满足要求。

如果看了这本书，只把设计模式背熟，然后“手里拿个锤子，看满世界都是钉子”，那就是买椟还珠了

我看到很多回答里都提到设计模式与JAVA的关系，认为设计模式是为JAVA搞的。

其实捋一下时间线，应该有更合理的解释。

《设计模式》成书于1995，JAVA上线也是1995。

这是巧合吗？不是。其实就是面向对象编程思想经历了十几年的大规模实践，业内对于正确的使用姿势形成了共识，而C++则是在共识之前形成的。

举个简单的例子，C++支持多继承，而JAVA则只支持单继承，但又搞出了接口实现这套东西，弥补单继承的不足，又不至于多继承的复杂性，这就是思想的演进。

因此，我更愿意相信，《设计模式》这本书是为C++写的，JAVA是为“设计模式”而发明的