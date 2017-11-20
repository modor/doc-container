####  1.maven源码目录下配置文件编译时无法复制问题。
在pom.xml中显式地告诉Maven把什么资源文件复制到target/classes文件夹下。 
```
<build>
    <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                 <includes>
                    <include>**/*.xml</include>
                    <include>**/*.properties</include>
                </includes>
            </resource>
     </resources>
</build>
```
####  2.hibernate和jdk版本问题。
* jdk1.7不支持 hibernate的最新版本5.2.0，使用jdk1.7时候把hibernate的版本换成5.1.3或更早的版本。
* mysql-connector-java-6.0.x也不被hibernate5.2.0支持，mysql驱动包换成5.1.40或更早的版本。