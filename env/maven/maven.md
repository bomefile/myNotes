 
 # scope 依赖范围
 
 > 既然，Maven 的生命周期存在编译、测试、运行这些过程，那么显然有些依赖只用于测试，比如 junit；有些依赖编译用不到，只有运行的时候才能用到，比如 mysql 的驱动包在编译期就用不到（编译期用的是 JDBC 接口），而是在运行时用到的；还有些依赖，编译期要用到，而运行期不需要提供，因为有些容器已经提供了，比如 servlet-api 在 tomcat 中已经提供了，我们只需要的是编译期提供而已。
 
 - compile：默认的 scope，运行期有效，需要打入包中。
 
 - provided：编译期有效，运行期不需要提供，不会打入包中。
 
 - runtime：编译不需要，在运行期有效，需要导入包中。（接口与实现分离）
 
 - test：测试需要，不会打入包中。
 
 - system：非本地仓库引入、存在系统的某个路径下的 jar。（一般不使用）
 
 mvn package -Dmaven.test.skip=true
 
 
 mvn archetype:generate DarchetypeGroupId=org.apache.maven.archetypes -DgroupId=com.mycompany.app -DartifactId=myapp
 
 mvn  [插件名]：[goal] [DarchetypeGroupId] 使用模版类型
 -DgroupId 相当于这个project的所有者或者机构的一个标识，一般是com.company.xxx这种格式
 -DartifactId 这个project最后所生成的文档(jar、war)的名字
  packaging： 这个project的打包的类型，一般是war、jar等值
  version： project的版本
  name： project的名字，生成文档等内容的时候会用的这个名字
 
 
 mvn compile 编译
 mvn package 打包
 /***********************************************************************************************************************************************/
 mvn site ： 为你的project创建一个站点
 mvn clean： 清除target目录下的所有文件
 mvn eclipse:eclipse ：为project生成eclipse的工程文件和classpath文件
 
 
 