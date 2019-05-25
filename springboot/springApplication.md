
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
   - 根据classpath判断服务的启动类型（org.springframework.web.servlet.DispatcherServlet）
   - ApplicationContextInitializer 创建实例
   - ApplicationListener 创建实例
   - 推断main方法的定义类

