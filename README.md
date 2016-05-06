# Spring
##### IOC原理（Inversion of Control）
解析xml（或注解）+反射

##### AOP原理（Aspect Oriented Programming）
动态代理（反射+代理模式）

# 反射
主要依赖的包：java.lang.reflect.*
主要依赖的类：Class,Constructer,Field,Method

# 代理
##### 静态代理
由程序员创建或特定工具自动生成源代码，再对其编译。在程序运行前，代理类的.class文件就已经存在了。

##### 动态代理（jdk和cglib）
在程序运行时，运用反射机制动态创建而成。 
jdk
cglib
