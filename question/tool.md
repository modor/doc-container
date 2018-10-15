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
