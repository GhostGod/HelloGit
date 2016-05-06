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
