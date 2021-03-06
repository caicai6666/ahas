# Spring Boot 应用接入 {#concept_bl5_lhq_bhb .concept}

通过 SDK 接入的方式，将 Spring Boot 应用接入 AHAS 控制台，使用流控降级服务。目前 AHAS 提供 Java SDK。

## 操作步骤 {#section_cbd_g3q_bhb .section}

为 Spring Boot 应用接入 AHAS 流控降级。

1.  在 pom.xml 文件中引入依赖：

    ```
    <dependency>
      <groupId>com.alibaba.csp</groupId>
      <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
      <!-- 可指定版本号，最新版本见 AHAS 控制台流控降级应用接入页引导。 -->
      <version>1.1.0</version>
    </dependency>
    ```

2.  在应用工程中加入类：

    ```
    @Configuration
    public class WebConfig {
      @Bean
      public FilterRegistrationBean sentinelFilterRegistration() {
        FilterRegistrationBean registration = new FilterRegistrationBean();
        registration.setFilter(new CommonFilter());
        //请根据实际情况配置要拦截的 URL Pattern
        registration.addUrlPatterns("*.json","*.hml","*.html","/demo/*");
        registration.setName("sentinelCommonFilter");
    	registration.setOrder(1);
        return registration;
      }
    }
    ```

3.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ```
        //将AppName替换为自定义的应用名称
        //通过公网地域接入时，需要您的证书信息；其他地域不需要证书。
        //证书获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 证书信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        在 application.properties 添加以下内容：

        ```
        #指定您要接入的特定的 AHAS 环境
        ahas.namespace=default
        #自定义您的应用名称
        project.name=AppName
        #通过公网地域接入时，需要您的证书信息；其他地域不需要证书。
        #证书获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的证书信息。
        ahas.license=xxx
        ```


应用接入配置完成后，需要应用有访问量，您才能在 AHAS 控制台的流控降级页面看到该应用。

## 后续操作 {#section_ckr_l2j_kgb .section}

接入了 AHAS 的流控降级服务后，您可以进一步了解：

-    [实时监控应用数据](../cn.zh-CN/流控降级/控制台指南/实时监控应用数据.md#)
-    [流控规则](../cn.zh-CN/流控降级/控制台指南/流控规则.md#) 
-   [降级规则](../cn.zh-CN/流控降级/控制台指南/降级规则.md#)
-    [系统规则](../cn.zh-CN/流控降级/控制台指南/系统规则.md#) 
-   [Java SDK 参考](../cn.zh-CN/流控降级/开发指南/Java SDK 参考/定义资源.md#)。

## 常见问题 {#section_umj_m2j_kgb .section}

如果您已完成流控降级服务接入，流控降级页面仍查看不到您的应用，可参考常见问题：[流控降级页面找不到应用](../cn.zh-CN/常见问题/流控降级常见问题.md#)。

