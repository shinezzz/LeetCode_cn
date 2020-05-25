# JDK源码

## 建议从JDK源码开始读起

1. List接口和ArrayList、LinkedList实现，HashMap和TreeMap
2. ArrayList和Vector
3. 《Java In A Nutshell》，里面有整个Java IO的架构图。
4. 读这些源码时，只需要读懂一些核心类即可，如和ArrayList类似的二三十个类，对于每一个类，也不一定要每个方法都读懂。

## Java Web项目源码阅读

表结构 → web.xml → mvc → db → spring ioc → log→ 代码

## Java框架源码阅读

在读Spring源码前，一定要先看看《J2EE Design and Development》这本书，它是Spring的设计思路。注意，不是中文版，中文版完全被糟蹋了。

## 一种可能的阅读顺序

基本类型的包装类(Character放在最后)
String、StringBuffer、StringBuilder、StringJoiner、StringTokenizer(补充正则表达式的知识)
CharacterIterator、StringCharacterIterator、CharsetProvider、CharsetEncoder、CharsetDecoder(较难)
java.util.function下的函数表达式
java.nio下的各种Buffer实现
java.lang.ref和jdk.internal.ref下的各种引用：软引用/弱引用/虚引用
Unsafe的实现(JDK9之后有两个同名类，一个引用了另一个，建议放在一起阅读)
java.util.stream下的流式编程的实现(很难)
Thread和ThreadLocal
Math、Random、BigInteger、BigDecimal
java.lang.reflect下反射的实现(先掌握JDK 9之后引入的模块系统)
ClassLoader的实现
javax.lang.model下Java语言模型的实现(可以参考Java官方语法文档)
注解(需要彻底掌握)
Timer、ResourceBundle、Properties
时间日期类型(尤其是Java8新增的部分)
java.lang.reflect.Proxy， JDK默认的动态代理
java.util.concurrent并发包。先读原子类，再读锁的实现类，最后阅读那些并发工具的实现(很难)
集合框架，主要是三大类：List、Set、Map(先读非线程安全的实现，再读线程安全的实现)
网络编程(主要阅读Socket通信部分，后续可以阅读HttpClient的实现)
IO/NIO/BIO(很难)
Files、Path等文件操作工具类
sql、xml处理类/接口
