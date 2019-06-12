

# 走向注解驱动编程

## 注解驱动发展史

### 启蒙时代 SpringFramework1.x
注解方式在java5发布的，
@Documented
@Inherited

SpringFramework 1.2.0开始，支持注解

### 注解驱动过渡时代 SpringFramework2.x

    * 依赖注入Annotation：@Autowired；
    * 依赖查找Annotation：@Qualifier；逻辑限定
    * 组件声明Annotation：@Component
    * SpringMVC Annotation：@Controller、@RequestMapping、@ModelAttribute、@RequestParam等。
    * @Service 数据相关的@Repository AOP相关的@Aspect
    * @PostConstruct 相当于<bean init-method = "..."/> 或 Spring InitializingBean接口回调
    * @PreDestroy 相当于<bean destory-method = "..."/> 或 Spring DisposableBean
    
````
<context:annotatiion-config/> :注册Annotation处理器
<context:component-scan/>：负责扫描相对于ClassPath下的指定Java根包，寻找被Spring模式注解标记的类，
将他们注册成Spring Bean
````

问题：@Bean 和 @Component 什么区别？
当时还在使用Struts2开发，SpringMVC 开始爆发。
---
### 注解驱动黄金时代：SpringFramework 3.x

1. 全面支持Java5（泛型、变量参数）。

2. 引入注解@Configuration 派生自 @Component

> 没有引入<context:component-scan> 注解，选择过渡方案@Import @ImportResource

````
    <import "xxx.xml"/>
    
    @Configuration
    @Import(MockConfiguration)
    public class XConfig(){
        
    }
````
> 通常标注@ImportResource或@Import的类需要再标注@Configuration

引出了一个新问题，SpringContextConfiguration有谁来引导？

3.0 引入 AnnotationConfigApplicationContext

引入注解

@Lazy
<bean lazy-init="true|false"
 @Primary 
 @DependsOn

3.1 脱胎换骨

<context:component-scan />
@Bean 和其搭配的@Role
@Profile 上下文条件话Bean定义

````
@Profile（"!production"）// 非生产环境
public class SpringContextConfiguration{
    ...
}


````
 
 