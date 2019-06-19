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

Spring Framework 外部依赖于容器配置启动。
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

依赖引入,springboot打包成fatjar
````
<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
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

Q:build-info是什么？
A:服务器监控信息。

target 包目录结构
````
wangliangliangdeMacBook-Pro:target wangliangliang$ tree -h
.
├── [ 160]  classes
│   ├── [  96]  META-INF
│   │   └── [ 188]  build-info.properties
│   ├── [ 299]  application.properties
│   └── [  96]  com
│       └── [  96]  test
│           └── [  96]  demofirstboot
│               └── [1.0K]  DemoFirstBootApplication.class
├── [ 17M]  demo-first-boot-0.0.1-SNAPSHOT.jar
├── [3.3K]  demo-first-boot-0.0.1-SNAPSHOT.jar.original
├── [  96]  generated-sources
│   └── [  64]  annotations
├── [  96]  generated-test-sources
│   └── [  64]  test-annotations
├── [  96]  maven-archiver
│   └── [  67]  pom.properties
├── [  96]  maven-status
│   └── [ 128]  maven-compiler-plugin
│       ├── [  96]  compile
│       │   └── [ 128]  default-compile
│       │       ├── [  54]  createdFiles.lst
│       │       └── [ 124]  inputFiles.lst
│       └── [  96]  testCompile
│           └── [ 128]  default-testCompile
│               ├── [   0]  createdFiles.lst
│               └── [ 129]  inputFiles.lst
├── [ 128]  surefire-reports
│   ├── [ 20K]  TEST-com.test.demofirstboot.DemoFirstBootApplicationTests.xml
│   └── [ 353]  com.test.demofirstboot.DemoFirstBootApplicationTests.txt
└── [  96]  test-classes
    └── [  96]  com
        └── [  96]  test
            └── [  96]  demofirstboot
                └── [ 661]  DemoFirstBootApplicationTests.class

21 directories, 13 files

````
├── [ 17M]  demo-first-boot-0.0.1-SNAPSHOT.jar 加工后的文件
├── [3.3K]  demo-first-boot-0.0.1-SNAPSHOT.jar.original 原始maven包结构，未包含第三方依赖资源

demo-first-boot-0.0.1-SNAPSHOT 目录结构
````
wangliangliangdeMacBook-Pro:demo-first-boot-0.0.1-SNAPSHOT wangliangliang$ tree
.
├── BOOT-INF
│   ├── classes
│   │   ├── application.properties
│   │   └── com
│   │       └── test
│   │           └── demofirstboot
│   │               └── DemoFirstBootApplication.class
│   └── lib
│       ├── HdrHistogram-2.1.9.jar
│       ├── LatencyUtils-2.0.3.jar
│       ├── classmate-1.4.0.jar
│       ├── hibernate-validator-6.0.16.Final.jar
│       ├── jackson-annotations-2.9.0.jar
│       ├── jackson-core-2.9.8.jar
│       ├── jackson-databind-2.9.8.jar
│       ├── jackson-datatype-jdk8-2.9.8.jar
│       ├── jackson-datatype-jsr310-2.9.8.jar
│       ├── jackson-module-parameter-names-2.9.8.jar
│       ├── javax.annotation-api-1.3.2.jar
│       ├── jboss-logging-3.3.2.Final.jar
│       ├── jul-to-slf4j-1.7.26.jar
│       ├── log4j-api-2.11.2.jar
│       ├── log4j-to-slf4j-2.11.2.jar
│       ├── logback-classic-1.2.3.jar
│       ├── logback-core-1.2.3.jar
│       ├── micrometer-core-1.1.4.jar
│       ├── slf4j-api-1.7.26.jar
│       ├── snakeyaml-1.23.jar
│       ├── spring-aop-5.1.7.RELEASE.jar
│       ├── spring-beans-5.1.7.RELEASE.jar
│       ├── spring-boot-2.1.5.RELEASE.jar
│       ├── spring-boot-actuator-2.1.5.RELEASE.jar
│       ├── spring-boot-actuator-autoconfigure-2.1.5.RELEASE.jar
│       ├── spring-boot-autoconfigure-2.1.5.RELEASE.jar
│       ├── spring-boot-starter-2.1.5.RELEASE.jar
│       ├── spring-boot-starter-actuator-2.1.5.RELEASE.jar
│       ├── spring-boot-starter-json-2.1.5.RELEASE.jar
│       ├── spring-boot-starter-logging-2.1.5.RELEASE.jar
│       ├── spring-boot-starter-tomcat-2.1.5.RELEASE.jar
│       ├── spring-boot-starter-web-2.1.5.RELEASE.jar
│       ├── spring-context-5.1.7.RELEASE.jar
│       ├── spring-core-5.1.7.RELEASE.jar
│       ├── spring-expression-5.1.7.RELEASE.jar
│       ├── spring-jcl-5.1.7.RELEASE.jar
│       ├── spring-web-5.1.7.RELEASE.jar
│       ├── spring-webmvc-5.1.7.RELEASE.jar
│       ├── tomcat-embed-core-9.0.19.jar
│       ├── tomcat-embed-el-9.0.19.jar
│       ├── tomcat-embed-websocket-9.0.19.jar
│       └── validation-api-2.0.1.Final.jar
├── META-INF
│   ├── MANIFEST.MF
│   ├── build-info.properties
│   └── maven
│       └── com.test
│           └── demo-first-boot
│               ├── pom.properties
│               └── pom.xml
└── org
    └── springframework
        └── boot
            └── loader
                ├── ExecutableArchiveLauncher.class
                ├── JarLauncher.class
                ├── LaunchedURLClassLoader$UseFastConnectionExceptionsEnumeration.class
                ├── LaunchedURLClassLoader.class
                ├── Launcher.class
                ├── MainMethodRunner.class
                ├── PropertiesLauncher$1.class
                ├── PropertiesLauncher$ArchiveEntryFilter.class
                ├── PropertiesLauncher$PrefixMatchingArchiveFilter.class
                ├── PropertiesLauncher.class
                ├── WarLauncher.class
                ├── archive
                │   ├── Archive$Entry.class
                │   ├── Archive$EntryFilter.class
                │   ├── Archive.class
                │   ├── ExplodedArchive$1.class
                │   ├── ExplodedArchive$FileEntry.class
                │   ├── ExplodedArchive$FileEntryIterator$EntryComparator.class
                │   ├── ExplodedArchive$FileEntryIterator.class
                │   ├── ExplodedArchive.class
                │   ├── JarFileArchive$EntryIterator.class
                │   ├── JarFileArchive$JarFileEntry.class
                │   └── JarFileArchive.class
                ├── data
                │   ├── RandomAccessData.class
                │   ├── RandomAccessDataFile$1.class
                │   ├── RandomAccessDataFile$DataInputStream.class
                │   ├── RandomAccessDataFile$FileAccess.class
                │   └── RandomAccessDataFile.class
                ├── jar
                │   ├── AsciiBytes.class
                │   ├── Bytes.class
                │   ├── CentralDirectoryEndRecord.class
                │   ├── CentralDirectoryFileHeader.class
                │   ├── CentralDirectoryParser.class
                │   ├── CentralDirectoryVisitor.class
                │   ├── FileHeader.class
                │   ├── Handler.class
                │   ├── JarEntry.class
                │   ├── JarEntryFilter.class
                │   ├── JarFile$1.class
                │   ├── JarFile$2.class
                │   ├── JarFile$JarFileType.class
                │   ├── JarFile.class
                │   ├── JarFileEntries$1.class
                │   ├── JarFileEntries$EntryIterator.class
                │   ├── JarFileEntries.class
                │   ├── JarURLConnection$1.class
                │   ├── JarURLConnection$JarEntryName.class
                │   ├── JarURLConnection.class
                │   ├── StringSequence.class
                │   └── ZipInflaterInputStream.class
                └── util
                    └── SystemPropertyUtils.class

18 directories, 98 files
````

* BOOT-INF/classes 存放编译后的classes文件
* BOOT-INF/lib 依赖的jar包
* META-INF 存放目录相应的元信息，MANIFEST.MF
* org SpringBoot相关的classes文件

````

wangliangliangdeMacBook-Pro:target wangliangliang$ tree original/
original/
├── META-INF
│   ├── MANIFEST.MF
│   ├── build-info.properties
│   └── maven
│       └── com.test
│           └── demo-first-boot
│               ├── pom.properties
│               └── pom.xml
├── application.properties
└── com
    └── test
        └── demofirstboot
            └── DemoFirstBootApplication.class

7 directories, 6 files
````



记得WEB-INF/classes 和 WEB-INF/lib下吗？


## jar 启动的秘密
````
META-INF的MANIFEST.MF

Manifest-Version: 1.0
Implementation-Title: demo-first-boot
Implementation-Version: 0.0.1-SNAPSHOT
Start-Class: com.test.demofirstboot.DemoFirstBootApplication
Spring-Boot-Classes: BOOT-INF/classes/
Spring-Boot-Lib: BOOT-INF/lib/
Build-Jdk-Spec: 1.8
Spring-Boot-Version: 2.1.5.RELEASE
Created-By: Maven Archiver 3.4.0
Main-Class: org.springframework.boot.loader.JarLauncher
````

---
理解固化的Maven依赖
---

## spring-boot-starter-parent 与 spring-boot-dependencies

spring-boot-starter-parent 存在一定的限制，很可能应用的pom 拥有自定义的Parent。

采用spring-boot-dependencies做依赖配置。
````
<!--<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>${spring.boot.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>-->
````

查看spring-boot-starter-parent的依赖关系，发现spring-boot-dependencies是其父类。

* spring-boot-starter-parent 
> 包含maven插件配置.可不添加repackage配置，仍可独立运行。

* spring-boot-dependencies
> 包含spring-boot依赖包的统一配置
  > SpringBoot maven配置
  > 打包成一个可执行的jar或war
````
 <plugin>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-maven-plugin</artifactId>
     <configuration>
         <executable>true</executable>
     </configuration>

     <executions>
         <execution>
             <goals>
                 <goal>repackage</goal>
             </goals>
         </execution>
     </executions>
 </plugin>
 
````
注意必须添加repackage否则打包的jar无法使用java -jar 运行

[更多介绍](https://docs.spring.io/spring-boot/docs/2.1.5.RELEASE/maven-plugin/)

---
理解嵌入式Web容器
---

Servlet规范 | Tomcat | Jetty | Undertow
---------| -------------
4.0 | 9.x | 9.x | 2.x
3.1 | 8.x | 8.x | 1.x
3.0 | 7.x | 7.x | N/A
2.5 | 6.x | 6.x | N/A

嵌入式容器如何启动？


从servlet3.0开始，Servlet组件通过ServletAPI在装配式运行。

ServletContainerInitializer 启动回调
WebApplicationInitializer springframework的抽象

在Spring Web自动装配中将详细说明。

## 变更spring默认的Servlet容器配置

````
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
			<version>${spring-boot.version}</version>
            <exclusions>
                <exclusion>
                    <groupId>org.springframework.boot</groupId>
					<artifactId>spring-boot-starter-tomcat</artifactId>
                </exclusion>
            </exclusions>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-jetty</artifactId>
			<version>2.1.3.RELEASE</version>
		</dependency>

````
---
理解自动装配
---

Q:什么是自动装配？

> Spring Boot auto-configuration attempts to automatically configure your Spring application based on the jar dependencies that you have added.
> For example, if HSQLDB is on your classpath, and you have not manually configured any database connection beans, then Spring Boot auto-configures an in-memory database.

查看官方文档的说明 16.Auto-Configuration


* @SpringBootConfiguration

* @EnableAutoConfiguration

* @Configuration


下面是SpringFramework常见的装配
````
<context:component-scan>

@ComponentScan

@Import

```` 
1. bean 收集注册

手动注册配置
````
    <bean id="mockService" class="...MockServiceImpl"/>
````
自动扫描配置
````    
    <context:commpent-scan base-package = "com.demo"/>
````
springboot配置
````
    @Configuration
    public void MockConfig{
        // bean 定义
        
        @Bean
        public MockService mockService(){
            new MockServiceImpl(dependencyService());// 注入
        }
        
        @Bean
        public DependencyService dependencyService(){
            new DependencyServiceImpl();
        }
    }
````

* @Properties @Property

> 从指定地方加载配置文件，并将其中的属性加载到IoC容器中，便于填充一些bean定义属性的占位符（placeholder），需要PropertiesSourcesPlaceholderConfigurer的配合
````
    @Configturation
    @PropertySource("classpath:1.properties")
    @PropertySource("classpath:2.properties")
    public class XConfiguration{
        
    }
````

* @Import @ImportResource

````
    <import "xxx.xml"/>
    
    @Configuration
    @Import(MockConfiguration)
    public class XConfig(){
        
    }
````
借助@Import() 将符合条件的@Configuration装载到springBoot的配置中
````
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)

````

## @SpringBootApplication

* @SpringBootConfiguration
    * @Configuration 代表定义了一个bean
* @EnableAutoConfiguration
    * @AutoConfigurationPackage
    * @Import(AutoConfigurationImportSelector.class)
    借助Import,将所有符合自动配置条件的bean定义加载到IoC容器中。
    AutoConfigurationImportSelector通过SpringFactoriesLoader
* @ComponentScan(
      excludeFilters = {@Filter(
      type = FilterType.CUSTOM,
      classes = {TypeExcludeFilter.class}
  ), @Filter(
      type = FilterType.CUSTOM,
      classes = {AutoConfigurationExcludeFilter.class}
  )}
  )
    * TypeExcludeFilter.class
     > springboot1.4引入，用于在beanFactory已注册的TypeExcludeFilter Bean
    * AutoConfigurationExcludeFilter
    > 1.5开始支持，用于排除其他同时标注@Configuration和@EnableAutoConfiguration的类


### @SpringBootConfiguration


* @Component
    * Configuration
        * SpringBootConfiguration
> 多层次@Component派生，官方称Spring模式注解（Stereotype Annotation），类似这样的有很多比如@Repository、@Service、@Controller
````
<context:component-scan base-package="com.paipai.inspect">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
        <context:exclude-filter type="annotation" expression="org.springframework.web.bind.annotation.ControllerAdvice"/>
    </context:component-scan>
````
* @AliasFor
> 用于桥接其他注解属性，能够将一个或多个注解的属性"别名"在某个注解中。这里存在Spring注解属性别名和覆盖，将在后续章节说明。

总结：@SpringbootApplication是一个聚合注解，包含@ComponentScan、@Configuration和@EnableAutoConfiguration的核心特性。

## @EnableAutoConfiguration 激活自动装配

源码查看@EnableAutoConfiguration的派生体系
演示实例：demo-first-boot

总结：SpringApplication#run方法引导Spring Boot应用时，并不强依赖于@Configuration类。
@EnableAutoConfiguration于@SpringBootApplication在激活自动装配方面没有差别的，然而对于被标注类的Bean类型存在差异。

## @SpringBootConfiguration "继承" @Configuration CGLIB提升特性

@Bean 在 @Component 和 @Configuration 差别
参考文档Spring-code文档 1.10.5

Full @Configuration vs “lite” @Bean mode?

在@Configuration中的bean为Full，会执行CGLIB提升

## 理解自动装配机制

SpringBoot官方文档49章节介绍基本的说明

通常与@Conditional注解关联使用

* @ConditionOnClass 当类存在于classpath下时
* @ConditionOnMissBean 当bean不存在于当前beanFactory时

示例说明
````
@Configuration
@ConditionalOnClass({ DataSource.class, EmbeddedDatabaseType.class }) ①
@EnableConfigurationProperties(DataSourceProperties.class)
@Import({ DataSourcePoolMetadataProvidersConfiguration.class,
		DataSourceInitializationConfiguration.class })
public class DataSourceAutoConfiguration ②{

	@Configuration
	@Conditional(EmbeddedDatabaseCondition.class) ③
	@ConditionalOnMissingBean({ DataSource.class, XADataSource.class })
	@Import(EmbeddedDataSourceConfiguration.class) ⑤
	protected static class EmbeddedDatabaseConfiguration ④{

	}
}
````

org.hsqldb.jdbcDriver存在为起始点。

装配问题官方说明描述：49.1 Understanding Auto-configured Beans

> 那么如果我想自己定义一个自动装配如何做呢？
> 官方文档已说明：49.2 Locating Auto-configuration Candidates

demo演示

> demo-autoconfig

---
理解Production-Ready特性
---

为预生产做准备

Spring Boot Actuator 

## 理解"外部化的配置"

外部配置变量引入方式：
* Bean的@Value
* Spring Environment读取
* @ConfigurationProperties 绑定到结构化对象

参考如下文档
> 24. Externalized Configuration

## 理解"规约大于配置"

> Absolutely no code generation and no requirement for XML configuration.


---
结束语
---
总结：Spring Boot五大特写

* SpringBootApplication
* 自动装配
* 外部化配置
* Spring Boot Actuator
* 嵌入式Web容器