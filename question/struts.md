####  1.struts有哪几种action编写方式？
- 创建普通类，在配置文件里面配置。 
- 创建实现了Action接口的类。
- 创建继承了ActionSupport的类，主要使用该种方式。

####  2.struts有哪几种action的方法访问方式？
- 通过配置action的method属性。 
- 通过通配符的方式，使用最多的方式。
- 通过动态访问实现。