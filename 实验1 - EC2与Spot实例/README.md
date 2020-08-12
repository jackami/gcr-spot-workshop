# 实验1：EC2 与 Spot 实例

本实验通过部署一个 Web 网站，演示如何使用 EC2 Spot Fleet 进行 Spot 实例的申请，业务的部署。以及使用 Auto Scaling 结合 ALB进 行业务动态扩缩容。

对于 EC2 实例的回收，通过 Spot Fleet 进行了中断测试，并使用 Lambda 函数把正在被中断的 EC2 从负载均衡的目标组中移除。 
