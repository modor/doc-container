####  1.struts有哪几种action编写方式？
- 创建普通类，在配置文件里面配置。 
- 创建实现了Action接口的类。
- 创建继承了ActionSupport的类，主要使用该种方式。

####  2.struts有哪几种action的方法访问方式？
- 通过配置action的method属性。 
- 通过通配符的方式，使用最多的方式。
- 通过动态访问实现。

####  3.struts的type属性有几种？
- 默认为dispatcher。
- 重定向为redirect。
- 重定向到新的Action为redirectAction。

####  4.struts的Action获取表单数据的方式？
- ActionContext类。
- ServletActionContext类。
- 使用接口注入的方式，实现ServletRequestAware接口。

####  5.struts提供了哪几种数据封装方式？
- 属性封装，Action类中直接定义属性。
- 模型驱动封装，Action实现ModelDriven接口。
- 表达式封装，适用于list和map封装。