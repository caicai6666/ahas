# 如何结束 AHAS Agent 进程？ {#concept_100074_zh .concept}

AHAS 为应用高可用探针（即 AHAS Agent）提供进程自动拉起功能，即定时检查 AHAS Agent 进程是否存在，如不存在，自动拉起该进程。这一功能保证了进程可用性，避免进程因异常挂掉或机器重启等原因，需要手动拉起的情况。

所以，您在服务器进程中结束 AHAS Agent 无法永久结束该进程，AHAS 会在定时检查后或机器重启时，自动拉起该进程。

如果您某段时间不需要使用 AHAS Agent，建议您登录[AHAS 控制台](https://ahas.console.aliyun.com)，在**管理**页面卸载 AHAS Agent。

