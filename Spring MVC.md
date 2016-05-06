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
