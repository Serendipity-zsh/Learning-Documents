#Spring学习笔记

###1、POJO：

全称是Plain Ordinary Java Object / Pure Old Java Object，中文可以翻译成：普通Java类，具有一部分getter/setter方法的那种类就可以称作POJO；

一般在web应用程序中建立一个数据库的映射对象时，我们只能称它为POJO；

一个POJO是一个不受任何限制的Java对象（除了Java语言规范）。例如一个POJO不应该是：

1、扩展预定的类，如       public class Foo extends javax.servlet.http.HttpServlet { ...；

2、实现预定的接口，如   public class Bar implements javax.ejb.EntityBean { ...；

3、包含预定的标注，如   @javax.ejb.Entity public class Baz{ ...
然后，因为技术上的困难及其他原因，许多兼容POJO风格的软件产品或框架事实上仍然要求使用预定的标注，譬如用于更方便的持久化

### 2、JavaBean：

是一种JAVA语言写成的可重用组件。它的方法命名，构造及行为必须符合特定的约定：

1、这个类必须有一个公共的缺省构造函数；

2、这个类的属性使用getter和setter来访问，其他方法遵从标准命名规范；

3、这个类应是可序列化的；

4、一个java模型组件，他为使用java类提供了一种标准的格式，在用户程序和可视化管理工具中可以自动获得这种具有标准格式的类的信息，并能够创建和管理这些类。 

5、可以使应用程序更加面向对象，可以把数据封装起来，把应用的业务逻辑和显示逻辑分离开，降低了开发的复杂程度和维护成本！

6、是一种JAVA语言写成的可重用组件。为写成JavaBean，类必须是具体的和公共的，并且具有无参数的构造器。JavaBeans 通过提供符合一致性设计模式的公共方法将内部域暴露称为属性。众所周知，属性名称符合这种模式，其他Java 类可以通过自省机制发现和操作这些JavaBean 属性。

因为这些要求主要是靠约定而不是靠实现接口，所以许多开发者把JavaBean看作遵从特定命名约定的POJO。

### 小结：

 简而言之，当一个Pojo可序列化，有一个无参的构造函数，使用getter和setter方法来访问属性时，他就是一个JavaBean。

