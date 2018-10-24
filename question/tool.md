####  1.github使用
1）代码冲突：git pull；修改冲突内容；git push。  
2）代码回退：git log获取commitId；git reset --hard commitId。  
3）代码回退后退回之前版本：git reflog获取commitId；git reset --hard commitId。  
4）建立里程碑（版本发布）：进入github项目页面，点击release；然后点击Draft a new release；填写信息，点击publish release即可。  
5）老版本发布记得打一个Tag，老版本bug修改通过该Tag建立老版本的分支，然后修复后将分支合并到版本即可。分支合并可以本地merge后push到github，也可以将分支push到github，然后在github上合并。  

####  2.maven使用
1）生成maven工程目录：mvn archetype:generate。  
2）依赖冲突规则：间接依赖路径最短优先；pom文件中申明顺序优先。  
3）依赖继承：继承其他项目的pom请使用<parent></parent>标签。  

### 3.maven、m2eclipse、jdk和eclipse关系说明
m2eclipse是eclipse的一个插件，m2eclipse插件默认集成了嵌入式maven，也可以使用自定义maven和其配置文件（Maven选项的Installations和User Settings中设置）。当前m2eclipse中集成的嵌入式maven默认编译java源码使用的jdk是1.5版本，在通过m2eclipse创建maven工程时候会将版本信息写入.classpath文件，在eclipse开发时候就会引入1.5版本的jdk，当使用更高的jdk时候我们需要在pom.xml中的编译插件的地方进行自定义，m2eclipse插件会自动将更新信息同步到.classpath中，但eclipse可能没有集成该jdk版本，例如1.8，那么我们就需要在Java的Installed JREs中配置jdk。默认情况我们使用m2eclipse中集成的maven来编译，但是如果需要使用eclipse来编译代码，我们就需要配置其编译器，在Java的Compiler中配置其编译器版本，需要和开发版本的jdk一致。maven是通过插件形式来使用的，格式为：mvn [pluginName]:[goalName]，我们可以通过apache的插件页面的Goals Overview参数来查看插件支持的goal name。m2eclipse默认集成了一些常见的插件及其命令，但毕竟功能有限，更多功能需要通过查看插件使用来支持。