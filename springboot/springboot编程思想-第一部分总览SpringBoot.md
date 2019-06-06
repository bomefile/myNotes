---
第一部分 总览Spring Boot
---

## SpringFramework 时代

> IoC Container, Events, Resources, i18n, Validation, Data Binding, Type Conversion, SpEL, AOP.

[spring-core](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#spring-core)

* IoC(Inversion of Control)
* AOP

spring本身并非容器，必须随着JavaEE容器启动而装载。
## Spring Boot

什么是SpringBoot？

Spring Boot is the starting point for building all Spring-based applications. 
Spring Boot is designed to get you up and running as quickly as possible, 
with minimal upfront configuration of Spring.

- Provide a radically faster and widely accessible getting-started experience for all Spring development.
- Be opinionated out of the box but get out of the way quickly as requirements start to diverge from the defaults.
- Provide a range of non-functional features that are common to large classes of projects (such as embedded servers, security, metrics, health checks, and externalized configuration).
- Absolutely no code generation and no requirement for XML configuration.

---
理解独立的Spring应用
---
应用类型划分：
- web应用
    * Servlet Web
    > ContextLoaderListener 和 DispatcherServlet的启动。
    * Reactive Web
- 非web应用
服务提供、消息处理、调度任务
容器：
SpringBoot使用嵌入式容器启动，把容器作为应用的一部分。本质上它属于Spring应用上下文中的组件Beans，跟随Spring应用上下午启动并注册初始化。

# 创建SpringBoot


## 创建SpringBoot项目
* mvn archetype
````
mvn archetype:generate -DgroupId=thinking-in-spring-boot
-DartifactId=first-spring-boot-application -Dversion=1.0.0-SNAPSHOT
-DinteractiveMode=false
-Dpackage=thinking.in.spring.boot
````
* https://start.spring.io/


## spring boot 工程结构

````
 wangliangliangdeMacBook-Pro:Downloads wangliangliang$ tree -a demo-first-boot
 demo-first-boot
 ├── .gitignore
 ├── .mvn
 │   └── wrapper
 │       ├── MavenWrapperDownloader.java
 │       ├── maven-wrapper.jar
 │       └── maven-wrapper.properties
 ├── HELP.md
 ├── mvnw
 ├── mvnw.cmd
 ├── pom.xml
 └── src
     ├── main
     │   ├── java
     │   │   └── com
     │   │       └── test
     │   │           └── demofirstboot
     │   │               └── DemoFirstBootApplication.java
     │   └── resources
     │       ├── application.properties
     │       ├── static
     │       └── templates
     └── test
         └── java
             └── com
                 └── test
                     └── demofirstboot
                         └── DemoFirstBootApplicationTests.java
 
 16 directories, 11 files

````

* .gitignore
* Maven Wrapper
> The Maven Wrapper is an easy way to ensure a user of your Maven Build has everything necessary to
run your Maven build.
    * .mvn/wrapper/maven.jar
    > 一个非常小的二进制文件(48KB)。用于从Maven官方下载Maven二进制文件
    * mvnw 和 mvnw.cmd
    ````
     mvn clean install
     ./mvnw clean install
     ./mvnw.cmd clean install
    ````
配合使用spring-boot:run运行。    
* application.properties 配置文件
* SpringBoot Junit 测试文件

## 运行

* jar 运行

依赖引入
````
<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<executions>
					<execution>
						<goals>
							<goal>build-info</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
````
````
[INFO] --- maven-jar-plugin:3.1.2:jar (default-jar) @ demo-first-boot ---
[INFO] Building jar: /Users/wangliangliang/Downloads/git/demo/demo-first-boot/target/demo-first-boot-0.0.1-SNAPSHOT.jar
[INFO] 
[INFO] --- spring-boot-maven-plugin:2.1.5.RELEASE:repackage (repackage) @ demo-first-boot ---
[INFO] Replacing main artifact with repackaged archive

````
````
java -jar target/first-app-by-gui-0.0.1-SNAPSHOT.jar
````
* maven运行
````
mvn spring-boot:run
````


# 启动运行

META-INF的MANIFEST.MF
- Main-Class：org.springframework.boot.loader.JarLauncher
- Start—Class：
