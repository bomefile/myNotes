

# SpringBootConfiguration

什么是自动装配？

借助@Import() 将符合条件的@Configuration装载到springBoot的配置中
````
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)

````

@ConditionOnClass

@ConditionOnMissingBean

