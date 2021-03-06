# 接入 Dubbo 应用 {#concept_gz5_d3c_kgb .concept}

将 Dubbo 应用接入 AHAS 应用流控降级后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文将帮助您了解如何使用 SDK 方式将 Dubbo 应用接入应用流控降级。

## 操作步骤 {#section_ry5_m4d_bhb .section}

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。
2.  在左侧导航栏中选择**流控降级** \> **应用流控**。
3.  在应用列表页面右上角单击**新应用接入**，然后选择**SDK 接入** \> **Dubbo 应用接入**页签。

    在Dubbo 应用接入 页面查看 Pom 依赖最新版本和 license 信息（非公网地域中不需要）。

    ![Dubbo 应用接入](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92287/156871918358999_zh-CN.png)

4.  选择以下任意一种方式，在 Dubbo 应用中添加应用流控降级依赖。
    -   在 Dubbo 应用的 Pom 文件中添加以下依赖：

        ``` {#codeblock_ojc_mer_kt3}
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          <!-- 可指定版本号，最新版本见 AHAS 控制台流控降级应用接入页引导。 -->
          <version>x.y.z</version>
        </dependency>
        ```

        **说明：** 在Dubbo 应用接入页签查看 Pom 依赖最新版本，将 `x.y.z` 替换为新版本的版本号。

    -   添加 Jar 包依赖。

        在Dubbo 应用接入页面单击**请点此链接下载**下载压缩包，并将压缩包中的所有 JAR 包放置在 classpath 目录下。

5.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数。
    -   修改 Spring Property 配置文件。

        如果您正在使用 Spring，并且希望将配置写入 Spring Property 文件中，参照以下步骤：

        1.  在 pom.xml 中引入以下依赖：

            ``` {#codeblock_01f_8wm_1rq}
            <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
              <!-- 可指定版本号，最新版本见 AHAS 控制台流控降级应用接入页引导。 -->
              <version>x.y.z</version>
            </dependency>
            ```

            **说明：** 在Dubbo 应用接入页签查看 Pom 依赖最新版本，将 `x.y.z` 替换为新版本的版本号。

        2.  在 application.properties 配置文件中，配置如下：
6.  （可选）您可以自定义 Dubbo 应用触发限流、降级或系统保护规则时的 fallback 处理逻辑，自定义[`DubboFallback`](https://github.com/alibaba/Sentinel/blob/master/sentinel-adapter/sentinel-dubbo-adapter/src/main/java/com/alibaba/csp/sentinel/adapter/dubbo/fallback/DubboFallback.java) 接口并通过 `DubboFallbackRegistry` 注册即可。配置后，当 Dubbo 应用被限流/降级/系统保护时，AHAS 会将 `BlockException` 包装后抛出。详情请参见[Dubbo Adapter](intl.zh-CN/应用流控降级/开发指南/配置流控逻辑.md#section_rgg_4vj_kgb)。

    **说明：** 若未执行此步骤，当 Dubbo 应用触发流控降级规则时，默认抛出 `BlockException` 异常类的子类（触发流控规则，则抛出流控异常 `FlowException`；触发降级规则，则抛出降级异常 `DegradeException`）。


## 结果验证 {#section_j74_bjp_ap0 .section}

启动应用并调用配置埋点的方法。若该应用出现在 AHAS 控制台**流控降级** \> **应用流控**页面，且在该应用的监控详情页面有能看到配置埋点的方法，则说明接入成功。

## 后续操作 {#section_vw0_tp4_rut .section}

为应用配置流控降级规则请参见以下文档：

-   [流控规则](intl.zh-CN/应用流控降级/控制台指南/流控规则.md#)
-   [降级规则](intl.zh-CN/应用流控降级/控制台指南/降级规则.md#)
-   [系统规则](intl.zh-CN/应用流控降级/控制台指南/系统规则.md#)

