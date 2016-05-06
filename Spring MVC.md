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
