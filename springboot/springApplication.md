
# 笔记

## spring 回顾

1. bean 收集注册

手动注册配置
````
    <bean id="mockService" class="...MockServiceImpl"/>
````
自动扫描配置
````    
    <context:commpent-scan base-package = "com.demo"/>
````

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
## @SpringBootApplication

* @SpringBootConfiguration
    * @Configuration 代表定义了一个bean
* @EnableAutoConfiguration
    * @AutoConfigurationPackage
    * @Import(AutoConfigurationImportSelector.class)
    借助Import,将所有符合自动配置条件的bean定义加载到IoC容器中。
    AutoConfigurationImportSelector通过SpringFactoriesLoader
* @ComponentScan

> 表示一个配置（configuration）class，声明



## @configuration
代表一个bean配置文件

## 启动流程

1. 初始化SpringApplication
   - weApplicationType参数配置，根据classpath判断服务的启动类型（org.springframework.web.servlet.DispatcherServlet）
   - ApplicationContextInitializer 创建实例
   - ApplicationListener 创建实例
   - 推断main方法的定义类
   
2. 完成SpringApplication初始化后开始启动，调用SpringApplicationRunListener的started()方法
     
3. 调用SpringApplicationListener的starting()方法

4. 创建并配置当前SpringBoot的将要使用的Environment（包括配置要使用的PropertiesSources以及Profile）

5. 遍历SpringApplicationListener构建环境变量做环境变量调用listener的environmentPrepared()方法

6. 创建ApplicationContext根据初始化的weApplicationType，通过BeanUtils实例化bean，生成ConfigurableApplicationContext

7. SpringBootExceptionReporter 异常回调接口

8. prepareContext 
    - 添加环境变量对象
    - postProcessApplicationContext
    - 调用ApplicationContextInitializer的initialize方法
    - 调用SpringApplicationListener的contextPrepared方法
    - 应用系统参数注册
    - 获取系统的所有启动类
    - 启动Source类验证
    - 启动类根据注解解析处理
    - 执行SpringApplicationListener的contextLoaded方法
9. refreshContext 
    - refreshContext 调用spring的refresh方法，使用spring的对bean处理
    - 注册shutdownHook
    
10. afterRefresh方法

11. listeners.started()

12. callRunners
    - 调用commandRunner
    
13. listener.running        
