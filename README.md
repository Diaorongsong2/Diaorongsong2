<div align="center">

<h1>运维工程师 / SRE</h1>

Linux 出身，做 Kubernetes 集群运维、监控告警和 CI/CD 交付。<br/>
习惯把巡检、变更、发布、排障的每一步写成文档，再想办法自动化掉。

<br/>

<p><img src="https://img.shields.io/badge/-深圳-2f81f7?style=flat-square" alt="深圳"> <a href="mailto:diaorongsong@163.com"><img src="https://img.shields.io/badge/-diaorongsong@163.com-238636?style=flat-square" alt="Email"></a> <img src="https://komarev.com/ghpvc/?username=Diaorongsong2&label=views&color=6e7681&style=flat-square" alt="views"></p>

</div>

---

## 关于

从 Linux 系统管理起手，现在主要做容器化平台的日常运维：

- **集群**：K8s 节点维护、工作负载发布与回滚、存储和网络排查
- **观测**：Prometheus 抓取配置、Grafana 看板、Alertmanager 告警收敛
- **交付**：Jenkins 流水线、Harbor 镜像管理、Ansible 批量作业

排障最怕两件事：日志找不到，指标口径说不清。所以项目里尽量把这两块先写明白。

## 一条完整的交付链路

```mermaid
flowchart LR
    A[提交代码] --> B[Jenkins<br/>构建 / 单测]
    B --> C[Harbor<br/>镜像仓库]
    C --> D[K8s<br/>滚动发布 / 灰度]
    D --> E[Prometheus<br/>指标采集]
    E --> F[Grafana<br/>看板]
    E --> G[Alertmanager<br/>告警]
```

从提交到可观测，每一段在下面的仓库里都能找到对应的脚本或清单。

## 仓库导航

| 仓库 | 是什么 | 先看这个 |
|:--|---|---|
| **[Ruoyi-cloud-cicd](https://github.com/Diaorongsong2/Ruoyi-cloud-cicd)**<br/><sub>Jenkins · Harbor · K8s</sub> | RuoYi-Cloud 微服务从代码到 K8s 的整条交付记录，含灰度发布 | `Jenkinsfile`、`scripts/` |
| **[Dify-AI-SOP](https://github.com/Diaorongsong2/Dify-AI-SOP)**<br/><sub>Helm · StatefulSet · 备份恢复</sub> | Dify 大模型平台的私有化部署，依赖组件怎么排、数据怎么备 | 部署清单 |
| **[gpu-monitor](https://github.com/Diaorongsong2/gpu-monitor)**<br/><sub>DCGM · Prometheus · Grafana</sub> | GPU 监控。显卡在 Windows 宿主、Prometheus 在 K8s 集群，跨机器抓取 | 指标口径说明 |
| **[Aliyun-tea-ecommerce-SOP](https://github.com/Diaorongsong2/Aliyun-tea-ecommerce-SOP)**<br/><sub>ECS · ACK · SLB</sub> | 阿里云茶叶电商系统，ECS 自建中间件到 ACK 容器化的迁移 | 部署顺序图 |

## 踩过的坑

下面几条都是当时卡了不短时间的，怎么试错、最后怎么绕过去的，仓库里的 SOP 都记着。

**ACK 拉不动自建 Harbor 的镜像**

Harbor 用的是自签证书，节点上的信任也加了，照样 `ErrImagePull`。没在证书上继续折腾，最后在跳板机 `docker save` 出来，`ctr -n k8s.io images import` 直接导进节点。

**显卡在 Windows 上，Prometheus 在 K8s 里**

跨机器抓 `192.168.44.1:9400`。一开始去改 Operator 生成的 Secret，过几分钟就被 reconcile 改回去了，查了半天才发现改错了地方。后来走 `spec.additionalScrapeConfigs` 指向自己的 Secret，才稳住。

**后台上传大图报 413**

不是改一处就好。nginx 的 `client_max_body_size`、Spring 的 `max-file-size`、还有 SLB 带宽，三处得对得上，漏一个照样传不上去。

## 技术栈

**系统与容器**

<p><img src="https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black"> <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white"> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white"> <img src="https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white"> <img src="https://img.shields.io/badge/Helm-0F1689?style=flat-square&logo=helm&logoColor=white"></p>

**交付与监控**

<p><img src="https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white"> <img src="https://img.shields.io/badge/Harbor-60B932?style=flat-square&logo=harbor&logoColor=white"> <img src="https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white"> <img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white"> <img src="https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white"> <img src="https://img.shields.io/badge/DCGM_Exporter-76B900?style=flat-square&logo=nvidia&logoColor=white"></p>

**数据与云**

<p><img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white"> <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white"> <img src="https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white"> <img src="https://img.shields.io/badge/阿里云_ACP-FF6A00?style=flat-square&logo=alibabacloud&logoColor=white"></p>

## 最近在做的

- 把运维里的重复动作交给智能体：Dify 工作流加 MCP 接口，试着让巡检和排障少一点手工
- GPU 算力环境的可观测性：DCGM 指标怎么落到看板，告警阈值到底该定多少

---

<div align="center"><sub>把每次排障都写成文档，下次就不用再猜一遍</sub></div>
