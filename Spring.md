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
- 使用cglib实现动态代理，需要在MethodInterceptor实现类中定义代理行为。
```java
/**
 * General-purpose {@link Enhancer} callback which provides for "around advice".
 * @author Juozas Baliuka <a href="mailto:baliuka@mwm.lt">baliuka@mwm.lt</a>
 * @version $Id: MethodInterceptor.java,v 1.8 2004/06/24 21:15:20 herbyderby Exp $
 */
public interface MethodInterceptor extends Callback
{
    /**
     * All generated proxied methods call this method instead of the original method.
     * The original method may either be invoked by normal reflection using the Method object,
     * or by using the MethodProxy (faster).
     * @param obj "this", the enhanced object
     * @param method intercepted Method
     * @param args argument array; primitive types are wrapped
     * @param proxy used to invoke super (non-intercepted method); may be called
     * as many times as needed
     * @throws Throwable any exception may be thrown; if so, super method will not be invoked
     * @return any value compatible with the signature of the proxied method. Method returning void will ignore this value.
     * @see MethodProxy
     */
    public Object intercept(Object obj, java.lang.reflect.Method method, Object[] args, MethodProxy proxy) throws Throwable;
}
```
- Cglib是一个优秀的动态代理框架，它的底层使用ASM（JAVA字节码处理框架）在内存中动态的生成被代理类的子类。使用CGLIB即使被代理类没有实现任何接口也可以实现动态代理功能。但是不能对final修饰的类进行代理。
- 通过字节码技术为一个类创建子类，并在子类中采用方法拦截的技术拦截所有父类方法的调用。
         <JDK动态代理与CGLib动态代理均是实现Spring AOP的基础>

##### jdk和cglib区别
- 字节码创建方式：JDK动态代理通过JVM实现代理类字节码的创建，cglib通过ASM创建字节码
- 对被代理对象的要求：JDK动态代理要求被代理对象实现接口，cglib要求被代理对象未被final修饰
- 代理对象创建速度：JDK动态代理创建代理对象速度比cglib快
- 代理对象执行速度：JDK动态代理代理对象执行速度比cglib快

# Spring MVC
#### Spring MVC的核心组件
1. DispatcherServlet：中央控制器，把请求给转发到具体的控制类
2. Controller：具体处理请求的控制器
3. HandlerMapping：映射处理器，负责映射中央处理器转发给controller时的映射策略
4. ModelAndView：服务层返回的数据和视图层的封装类
5. ViewResolver：视图解析器，解析具体的视图
6. Interceptors ：拦截器，负责拦截我们定义的请求然后做处理工作

#### Spring MVC的核心工作流程

http://blog.csdn.net/daybreak1209/article/details/50663997

*request请求到中央控制器——>传到映射处理器——>转发到指定controller——>获取数据和view ，组成成ModelAndView组件——>通过ViewResolver返回到特定的前台页面*

# Spring Data JPA
#### 核心接口
1. Repository：最顶层的接口，是一个空的接口，目的是为了统一所有Repository的类型，且能让组件扫描的时候自动识别。
2. CrudRepository ：是Repository的子接口，提供CRUD的功能
3. PagingAndSortingRepository：是CrudRepository的子接口，添加分页和排序的功能
4. JpaRepository：是PagingAndSortingRepository的子接口，增加了一些实用的功能，比如：批量操作等。
5. JpaSpecificationExecutor：用来做负责查询的接口
6. Specification：是Spring Data JPA提供的一个查询规范，要做复杂的查询，只需围绕这个规范来设置查询条件即可

#### 对存储大数据的LOB类型，JPA只要在Entiry中注解@LOB即可

LOB 代表大对象数据，包括 BLOB 和 CLOB 两种类型，前者用于存储大块的二进制数据，如图片数据，视频数据等，而后者用于存储长文本数据，如论坛的帖子内容，产品的详细描述等。

值得注意的是：在不同的数据库中，大对象对应的字段类型是不尽相同的，如 DB2 对应 BLOB/CLOB，MySql 对应 BLOB/LONGTEXT，SqlServer 对应 IMAGE/TEXT。

需要指出的是，有些数据库的大对象类型可以象简单类型一样访问，如 MySql 的 LONGTEXT 的操作方式和 VARCHAR 类型一样。在一般情况下， LOB 类型数据的访问方式不同于其它简单类型的数据，我们经常会以流的方式操作 LOB 类型的数据。此外，LOB 类型数据的访问不是线程安全的，需要为其单独分配相应的数据库资源，并在操作完成后释放资源。

（参考：http://www.ibm.com/developerworks/cn/java/j-lo-spring-lob/）

# Spring Boot

https://qbgbook.gitbooks.io/spring-boot-reference-guide-zh/content/IV.%20Spring%20Boot%20features/29.1.1.%20Connecting%20to%20Redis.html
