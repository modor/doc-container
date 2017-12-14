####  1.Bean实例化的三种方式？
- 使用类的无参构造方法创建。
- 使用静态工厂创建。
- 使用实例工厂创建。

####  2.Scope属性值有哪些？
- singleton 默认值
- prototype
- request
- session
- globalSession(单点登录时候使用)

####  3.属性注入的三种方式是什么？
- 使用set方法方式。
- 使用构造方法注入方式。
- 接口注入方式。

### 4.spring在web项目中如何使用？
通过创建servletContext的监听器初始化spring，放到servletContext域对象当中，servlet通过域对象获取bean实例。

### 5.用来创建对象的注解有哪几个？
- @Componet：无法分层
- @Controller：web层
- @Service： 业务层
- @Repository： 持久层

### 5.通过什么注解配置单实例和多实例？
- @Scope(value="prototype")

### 6.如何进行注解注入对象？
- 属性上面加@Autowired注解。
- 属性上面加@Resource(name="对象注解value值")
