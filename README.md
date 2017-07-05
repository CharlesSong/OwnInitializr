#  Ⅰ.前言
使用IDE等工具通过 https://start.spring.io/  创建项目非常方便，但是限于网络原因，有时候无法访问。Spring Initializr提供了搭建个人Initialzr项目的支持，通过参考 http://blog.csdn.net/chszs/article/details/51713174  有很多细节没有描述清楚。

# Ⅱ.开始搭建

## 1. 通过 https://start.spring.io/ 创建一个Maven  web项目
![image](https://github.com/CharlesSong/OwnInitializr/screenshots/8cb0c021-2eec-4f17-9fa5-96fd8b8a5801.png)
## 2. 添加依赖
```
                <dependency>
			<groupId>io.spring.initializr</groupId>
			<artifactId>initializr-web</artifactId>
		</dependency>
```
## 3. 启动运行
运行报错，无法引入依赖。仔细查找文档，https://github.com/spring-io/initializr README中有说明：

 >简单翻译下：Spring Initializr没有在Maven仓库中提供，你需要自己从源码构建。

## 4. Clone源码，按照源码提示进行编译
```
//进入 initialzr项目目录，执行（好慢，我大概执行了1个小时）
./mvnw clean install

//备注：mvnw执行的是包装maven，未使用本地的maven，安装到maven默认仓库位置。如果本地maven仓库的位置不是默认的，在本地仓库下还是找不到依赖jar，可以在默认位置复制到本地即可。
```
执行成功结果

## 5.再次启动运行，异常
```
2017-07-05 10:33:51.265 ERROR 134836 --- [           main] o.s.b.f.s.DefaultListableBeanFactory     : Destroy method on bean with name 'org.springframework.boot.autoconfigure.internalCachingMetadataReaderFactory' threw an exception

java.lang.IllegalStateException: ApplicationEventMulticaster not initialized - call 'refresh' before multicasting events via the context: org.springframework.boot.context.embedded.AnnotationConfigEmbeddedWebApplicationContext@533bda92: startup date [Wed Jul 05 10:33:40 CST 2017]; root of context hierarchy
	at org.springframework.context.support.AbstractApplicationContext.getApplicationEventMulticaster(AbstractApplicationContext.java:414) [spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.support.ApplicationListenerDetector.postProcessBeforeDestruction(ApplicationListenerDetector.java:97) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.beans.factory.support.DisposableBeanAdapter.destroy(DisposableBeanAdapter.java:253) ~[spring-beans-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroyBean(DefaultSingletonBeanRegistry.java:578) [spring-beans-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroySingleton(DefaultSingletonBeanRegistry.java:554) [spring-beans-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.destroySingleton(DefaultListableBeanFactory.java:961) [spring-beans-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroySingletons(DefaultSingletonBeanRegistry.java:523) [spring-beans-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.destroySingletons(DefaultListableBeanFactory.java:968) [spring-beans-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.destroyBeans(AbstractApplicationContext.java:1030) [spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:556) [spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.boot.context.embedded.EmbeddedWebApplicationContext.refresh(EmbeddedWebApplicationContext.java:122) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:693) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:360) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:303) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1118) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1107) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at com.github.charles.OwnInitializrApplication.main(OwnInitializrApplication.java:10) [classes/:na]

2017-07-05 10:33:51.278  INFO 134836 --- [           main] utoConfigurationReportLoggingInitializer :

Error starting ApplicationContext. To display the auto-configuration report re-run your application with 'debug' enabled.
2017-07-05 10:33:51.287 ERROR 134836 --- [           main] o.s.boot.SpringApplication               : Application startup failed

org.springframework.beans.factory.BeanDefinitionStoreException: Failed to process import candidates for configuration class [io.spring.initializr.web.autoconfigure.InitializrAutoConfiguration]; nested exception is java.lang.ClassCastException: java.lang.ClassNotFoundException cannot be cast to [Ljava.lang.Object;
	at org.springframework.context.annotation.ConfigurationClassParser.processImports(ConfigurationClassParser.java:616) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassParser.doProcessConfigurationClass(ConfigurationClassParser.java:299) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassParser.processConfigurationClass(ConfigurationClassParser.java:245) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassParser.processImports(ConfigurationClassParser.java:606) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassParser.processDeferredImportSelectors(ConfigurationClassParser.java:548) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassParser.parse(ConfigurationClassParser.java:185) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassPostProcessor.processConfigBeanDefinitions(ConfigurationClassPostProcessor.java:308) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassPostProcessor.postProcessBeanDefinitionRegistry(ConfigurationClassPostProcessor.java:228) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.support.PostProcessorRegistrationDelegate.invokeBeanDefinitionRegistryPostProcessors(PostProcessorRegistrationDelegate.java:270) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.support.PostProcessorRegistrationDelegate.invokeBeanFactoryPostProcessors(PostProcessorRegistrationDelegate.java:93) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.invokeBeanFactoryPostProcessors(AbstractApplicationContext.java:687) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:525) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	at org.springframework.boot.context.embedded.EmbeddedWebApplicationContext.refresh(EmbeddedWebApplicationContext.java:122) ~[spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:693) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:360) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:303) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1118) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1107) [spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at com.github.charles.OwnInitializrApplication.main(OwnInitializrApplication.java:10) [classes/:na]
Caused by: java.lang.ClassCastException: java.lang.ClassNotFoundException cannot be cast to [Ljava.lang.Object;
	at org.springframework.boot.context.properties.EnableConfigurationPropertiesImportSelector.selectImports(EnableConfigurationPropertiesImportSelector.java:54) ~[spring-boot-1.5.4.RELEASE.jar:1.5.4.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassParser.processImports(ConfigurationClassParser.java:586) ~[spring-context-4.3.9.RELEASE.jar:4.3.9.RELEASE]
	... 18 common frames omitted
```
异常没有找到解决方案。补充：后来发现是编译缓存的问题。清楚缓存或者重建项目后，恢复正常。


 通过截图可以看出依赖等配置都是空的。

## 6.自定义配置
编辑application.yml配置文件。详见配置文件

#  Ⅲ.项目源码

#  Ⅳ.待解决问题
## 1.默认生成application.yml配置文件
在Issue中看到，现在并不支持默认生成application.yml。原因是IDE对yml支持不友好。
## 2.如何添加一些额外的信息到生成的项目中？比如：服务中心、配置中心的配置、通用jar包、数据库配置等





