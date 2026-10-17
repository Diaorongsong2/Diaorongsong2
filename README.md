### 刁荣松 · 运维工程师 / SRE

Linux 出身，做 Kubernetes 集群运维、监控告警和 CI/CD 交付。
习惯把巡检、变更、发布、排障的每一步写成文档，再想办法自动化掉。

目前在看深圳的运维 / SRE 机会。简历里的项目细节都在下面四个仓库里。
邮箱：diaorongsong@163.com

---

## 仓库导航

| 仓库 | 里面是什么 | 建议先看 |
|---|---|---|
| [Ruoyi-cloud-cicd](https://github.com/Diaorongsong2/Ruoyi-cloud-cicd) | RuoYi-Cloud 微服务从代码到 K8s 的完整交付记录：Jenkins 流水线、Harbor 镜像、K8s 编排、灰度发布 | `Jenkinsfile`、`scripts/` |
| [Dify-AI-SOP](https://github.com/Diaorongsong2/Dify-AI-SOP) | Dify 大模型平台的私有化部署：Helm values、StatefulSet、依赖组件、备份与恢复 | `README.md` 里的部署清单 |
| [gpu-monitor](https://github.com/Diaorongsong2/gpu-monitor) | DCGM Exporter + Prometheus + Grafana 的 GPU 监控。显卡在 Windows 宿主、Prometheus 在 K8s 集群，跨机器抓取，含指标口径说明 | `README.md` 的指标解释 |
| [Aliyun-tea-ecommerce-SOP](https://github.com/Diaorongsong2/Aliyun-tea-ecommerce-SOP) | 阿里云茶叶电商系统：ECS 自建中间件、ACK 容器化、SLB 对外发布 | 部署顺序那张图 |

## 常用技术栈

- 系统与容器：Linux（CentOS / Ubuntu）、Kubernetes、Docker、Nginx、Keepalived
- 交付流水线：Jenkins、GitLab CI、Harbor、Ansible、Shell、Python
- 监控告警：Prometheus、Grafana、Alertmanager、Zabbix、node-exporter、DCGM Exporter
- 中间件与存储：MySQL、Redis、Nacos、Sentinel、Kafka、ELK、MinIO、NFS
- 云：阿里云云计算工程师（ACP），ECS / ACK / SLB / OSS / VPC

## 最近在做的

- 把运维侧的重复操作交给智能体：Dify 工作流 + MCP 接口，试着让巡检和排障少一点手工
- GPU 算力环境的可观测性：DCGM 指标怎么落到看板，告警阈值该怎么定

<sub>主页访问计数（第三方统计，会稍有偏差）</sub>

![profile views](https://komarev.com/ghpvc/?username=Diaorongsong2&label=profile%20views&color=2f81f7&style=flat)
