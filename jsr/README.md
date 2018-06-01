## JSR编号和规范名称对应关系
编号          | 名称 
----   |------
JSR336 | Java SE 7         
JSR342 | Java EE 7  


## Java SE 7包含（Java SE JDK实现）的规范列表
编号          | 名称                                                                                                                                                 | 版本
----   |------                                                        |------
JSR292 |Support for dynamically-typed languages(InvokeDynamic)        |
JSR334 |Small language enhancements (Project Coin)                    |
JSR203 |More new I/O APIs for the Java platform (NIO.2)               |
JSR260 |Javadoc Tag Technology Update                                 |
JSR295 |Beans Binding                                                 |
JSR296 |Swing Application Framework                                   |
JSR305 |Annotations for Software Defect Detection                     |
JSR308 |Annotations on Java Types                                     |
JSR310 |Date and Time API                                             |
JSR114 |JDBC Rowsets                                                  |
JSR221 |JDBC 4.0                                                      |
JSR224 |Java API for XML Web Services                                 |
JSR269 |Pluggable Annotation-Processing API                           |
JSR901 |Java Language Specification                                   |
JSR924 |Java Virtual Machine Specification                            |


## Java EE 7包含（Java EE JDK实现）的规范列表
编号          | 名称                                                                                                                                                 | 版本
----   |------                                                        |------
Web Application Technologies:                                         |
JSR356 |Java API for WebSocket                                        |
JSR353 |Java API for JSON Processing                                  |
JSR340 |Java Servlet                                                  | 3.1
JSR344 |JavaServer Faces (JSF)                                        | 2.2
JSR341 |Expression Language (EL)                                      | 3.0
JSR245 |JavaServer Pages (JSP)                                        | 2.3
JSR52  |JavaServer Pages Standard Tag Library (JSTL)                  | 1.2
Enterprise Application Technologies:                                  |
JSR352 |Batch Applications for the Java Platform                      |
JSR236 |Concurrency Utilities for Java EE                             |1.0
JSR346 |Contexts and Dependency Injection for Java (CDI)              |1.1
JSR330 |Dependency Injection for Java                                 |1.0
JSR349 |Bean Validation                                               |1.1
JSR316 |Managed Beans                                                 |1.0
JSR345 |Enterprise JavaBeans (EJB)                                    |3.2
JSR318 |Interceptors                                                  |1.2
JSR322 |Java EE Connector Architecture                                |1.7
JSR338 |Java Persistence API (JPA)                                    |2.1
JSR250 |Common Annotations for the Java Platform                      |1.2
JSR343 |Java Message Service API (JMS)                                |2.0
JSR907 |Java Transaction API (JTA)                                    |1.2
JSR919 |JavaMail API                                                  |1.5
Web Services Technologies:                                            |
JSR339 |Java API for RESTful Web Services (JAX-RS)                    |2.0
JSR109 |Implementing Enterprise Web Services                          |1.4
JSR224 |Java API for XML-Based Web Services (JAX-WS)                  |2.2
JSR181 |Web Services Metadata for the Java Platform                   |
JSR101 |Java API for XML-based RPC (JAX-RPC) (Optional)               |1.1
JSR222 |Java Architecture for XML Binding (JAXB)                      |2.2
JSR93  |Java API for XML Registries (JAXR)                            |1.0
Management and Security Technologies:                                 |
JSR196 |Java Authentication Service Provider Interface for Containers |1.1
JSR115 |Java Authorization Service Provider Contract for Containers   |1.5
JSR88  |Java EE Application Deployment (Optional)                     |1.2
JSR77  |Java EE Management                                            |1.1
JSR45  |Debugging Support for Other Languages                         |1.0
Java EE-related Specs in Java SE: 								      |
JSR222 |Java Architecture for XML Binding (JAXB)                      |2.2
JSR206 |Java API for XML Processing (JAXP)                            |1.3
JSR221 |Java Database Connectivity                                    |4.0
JSR3   |Java Management Extensions (JMX)                              |2.0
JSR925 |JavaBeans Activation Framework (JAF)                          |1.1
JSR67  |Java APIs for XML Messaging                                   |1.3
JSR173 |Streaming API for XML (StAX)                                  |1.0

**JSR规范列表：** https://www.jcp.org/en/jsr/all


公司                                   | SUN          | Oracle     |Apache     | RedHat    | IBM              |开源社区                      |其他  
------           |------        |------      |------     |------     |------            |------         |------  
基于Java SE标准          |SunJDK        |            | Harmony   |           |                  |OpenJDK        | 
基于Java EE标准          |Glassfish     |WebLogic    |Geronimo   | JBoss     | Websphere        |               |   
基于Java NIO标准        |Grizzly       |            |Mina       | Netty     |                  |               |  
基于Restful标准          |Jersey        |            |cxf/wink   |           |                   |              |  
基于Servlet标准          |              |            |Tomcat     | RestEasy  | Jetty             |              |  
基于JMS标准                   |              |            |ActiveMq   |            |                  |               |  
基于RMI标准                   |              |            |           |            |                  |               |Dubbo  


**注：**   
* 由于Glassfish是由SUN基于Java EE做的参考实现，所以，到其官网下载Java EE SDK时候会把Glassfish一起下载下来，然后两者是不同的东西，Glassfish是基于Java EE SDK做出的产品。 Glassfish是开源的，遵循CDDL 1.0版本和GPL2.0版本，故Java EE SDK也是开源的，只要遵循开源协议便没有版权问题。  
* 但Java SE SDK却分为SUN JDK和OPEN JDK，所以，到Oracle官网上下载的Java SE SDK是存在版权风险的。  
* 虽说Java EE开源，但各个厂商为了规避风险，所使用的Java EE基础库都是根据JSR自己实现的。比如，tomcat所用的jar是tomcat开发人员自己实现的servlet标准，jboss所使用的的Java EE基础库则是Jboss社区自己根据JSR自己实现。  
* 另外，RedHat讲Jboss的名字改叫WildFly（真难听）了。还有，有些实现是包含与被包含的关系，比如，Java EE容器里面一般都实现了servlet，Restful这些被JSR342包含的内容，但大多数情况用不到Java EE的全部标准，于是像Tomcat和Jersey只实现了Java EE当中的servlet和restful标准。  










