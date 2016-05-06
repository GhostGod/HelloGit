# Hibernate
hibernate是一个采用ORM（Object/Relation Mapping对象关系映射）机制持久层的开源框架

#### 核心接口
- Configuration接口，用于读取配置文件信息(hibernate.cfg.xml)，创建SessionFactory.(注意如果:hibernate.cfg.xml的名字改了以后要写在:Configuration config = new Configuration().configure("a.xml");否则他找不到)
- SessionFactory接口:用来生厂Session对象
- Session接口:封装Connection对象,他还提供了对数据持久化对象进行操作的方法，可以把它想象成一个持久对象的缓冲区，Hibernate能够自动检测缓冲区中的持久化对象是否已经改变，并及时刷新数据库，以保证Session中的对象与数据库同步
- Transaction接口：事物对象(增删改)\一般在Oracle中使用(必须添加事务)
- Query接口：对数据库以及持久化对象进行查询
- Criteria接口：他允许创建并执行面向对象的标准化查询(对象查询)

#### 3种数据状态
- 瞬时状态：当实例化一个持久化对象后，这个对象就处于瞬时状态。即保存在一个内存区域
- 持久状态:当Hibernate核心API把处于瞬时状态的持久化对象与数据库中的数据进行关联，对象具有了唯一的OID标识，那么就为持久状态
- 游离状态：当Hibernate核心API的Session关闭后，此次持久化对象虽然拥有了OID和数据库对应的记录，但是会话已经关闭，对象不再持久化管理之内，此时就叫游离状态

# Hibernate Validator
#### 验证注解
- @AssertTrue //用于boolean字段，该字段只能为true  
- @AssertFalse//该字段的值只能为false  
- @CreditCardNumber//对信用卡号进行一个大致的验证  
- @DecimalMax//只能小于或等于该值  
- @DecimalMin//只能大于或等于该值  
- @Digits(integer=2,fraction=20)//检查是否是一种数字的整数、分数,小数位数的数字。  
- @Email//检查是否是一个有效的email地址  
- @Future//检查该字段的日期是否是属于将来的日期  
- @Length(min=,max=)//检查所属的字段的长度是否在min和max之间,只能用于字符串  
- @Max//该字段的值只能小于或等于该值  
- @Min//该字段的值只能大于或等于该值  
- @NotNull//不能为null  
- @NotBlank//不能为空，检查时会将空格忽略  
- @NotEmpty//不能为空，这里的空是指空字符串  
- @Null//检查该字段为空  
- @Past//检查该字段的日期是在过去  
- @Size(min=, max=)//检查该字段的size是否在min和max之间，可以是字符串、数组、集合、Map等  
- @URL(protocol=,host,port)//检查是否是一个有效的URL，如果提供了protocol，host等，则该URL还需满足提供的条件  
- @Valid//该注解只要用于字段为一个包含其他对象的集合或map或数组的字段，或该字段直接为一个其他对象的引用，这样在检查当前对象的同时也会检查该字段所引用的对象
*注解中的message支持从配置文件中读取ValidationMessages_zh_CN.properties，配置文件中也支持表达式*
#### 自定义约束
http://docs.jboss.org/hibernate/validator/5.2/reference/en-US/html/ch06.html

#### 手动调用validator
```java
ValidatorFactory factory = Validation.buildDefaultValidatorFactory();  
        Validator validator = factory.getValidator();  
  
        Entity entity = new Entity();  
        entity.setAge(12);  
        entity.setName("admin");  
        Set<ConstraintViolation<Entity>> constraintViolations = validator.validate(entity);  
        for (ConstraintViolation<Entity> constraintViolation : constraintViolations) {  
            System.out.println("对象属性:"+constraintViolation.getPropertyPath());  
            System.out.println("国际化key:"+constraintViolation.getMessageTemplate());  
            System.out.println("错误信息:"+constraintViolation.getMessage());  
        }  
```
