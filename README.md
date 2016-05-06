# Spring
##### IOC原理（Inversion of Control）
解析xml（或注解）+反射

##### AOP原理（Aspect Oriented Programming）
动态代理（反射+代理模式）

# 反射
- 主要依赖的包：java.lang.reflect.*
- 主要依赖的类：Class,Constructer,Field,Method

# 代理模式
##### 静态代理
由程序员创建或特定工具自动生成源代码，再对其编译。在程序运行前，代理类的.class文件就已经存在了。

##### 动态代理（jdk和cglib）
在程序运行时，运用反射机制动态创建而成。 

###### jdk动态代理（包含一个类和一个接口）
```java
public interface InvocationHandler { 
   /**
	 * @param proxy 指被代理的对象
	 * @param method 要调用的方法
	 * @param args 方法调用时所需要的参数
	 * @return
	 * @throws Throwable
	 */
  public Object invoke(Object proxy,Method method,Object[] args) throws Throwable; 
}

	/**
	 * Proxy类是专门完成代理的操作类，可以通过此类为一个或多个接口动态地生成实现类，此类提供了如下的操作方法
	 * @param loader 类加载器
	 * @param interfaces 得到全部的接口
	 * @param h 得到InvocationHandler接口的子类实例
	 * @return
	 * @throws IllegalArgumentException
	 */
public static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces, InvocationHandler h) throws IllegalArgumentException
```
类加载器,在Java中主要有以下3种类加载器
- Booststrap ClassLoader：此加载器采用C++编写，一般开发中是看不到的
- Extendsion ClassLoader：用来进行扩展类的加载，一般对应的是jre\lib\ext目录中的类
- AppClassLoader：(默认)加载classpath指定的类，是最常使用的是一种加载器
- 允许自定义类加载器
###### cglib动态代理
