# Spring
#### IOC原理（Inversion of Control）
解析xml（或注解）+反射

#### AOP原理（Aspect Oriented Programming）
动态代理（反射+代理模式）

# 反射
- 主要依赖的包：java.lang.reflect.*
- 主要依赖的类：Class,Constructer,Field,Method

# 代理模式
#### 静态代理
由程序员创建或特定工具自动生成源代码，再对其编译。在程序运行前，代理类的.class文件就已经存在了。

#### 动态代理（jdk和cglib）
字节码是在程序运行时由Java反射机制动态生成。

##### jdk动态代理[对有实现接口的对象做代理]
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
###### 类加载器,在Java中主要有以下3种类加载器允许自定义类加载器
- 引导类加载器Booststrap ClassLoader：此加载器采用C++编写，一般开发中是看不到的
- 扩展类加载器Extendsion ClassLoader：用来进行扩展类的加载，一般对应的是jre\lib\ext目录中的类
- 系统类加载器AppClassLoader：(默认)加载classpath指定的类，是最常使用的是一种加载器

##### cglib动态代理[对没有实现接口的普通类做代理]
- Cglib是一个优秀的动态代理框架，它的底层使用ASM（JAVA字节码处理框架）在内存中动态的生成被代理类的子类。使用CGLIB即使被代理类没有实现任何接口也可以实现动态代理功能。但是不能对final修饰的类进行代理。
- 通过字节码技术为一个类创建子类，并在子类中采用方法拦截的技术拦截所有父类方法的调用。
         <JDK动态代理与CGLib动态代理均是实现Spring AOP的基础>
