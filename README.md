# 背景

#### 领域现状

- 缺陷/用例管理平台多
- 过程重管理，轻分析
- 结果重数据，轻过程
- 操作上依赖平台熟练程度
- 执行上依赖领域技术知识
- 总结上依赖领域管理知识
- 软件质量管理经验者较少
- 工具传承重于经验传承
- 没有一套可复用的标准

#### 我们的目标

**打造一个软件质量保障平台**

- 对接市场已有平台
- 制定标准
- 传承经验
- 软件质量统一评级
- 软件质量趋势分析
- 软件质量风控告警
- 低学习成本

# 愿景

**简单度量简单管理**

**分享软件质量保障的配方，把冷冰冰的数据变成有情感的健康指标**

# 架构

# 功能

#### 配置管理

用于配置连接缺陷管理服务器和用例管理服务器的信息，如 JIRA「已部分支持」、禅道「暂不支持」、Bugzilla「暂不支持」、TestLink「暂不支持」。

#### 项目管理

只需要定义项目名称和关联所在的服务器，项目名称应当与所在服务器上的项目同名。

#### 迭代管理

管理迭代信息，信息量较大，所有信息都应与服务器上同名。提供默认值以反向指导用户如何规划缺陷管理服务器和用例管理服务器。

#### 同步

默认每小时自动与服务器同步数据，可额外对每个迭代进行手动同步操作，激活状态的迭代同步时会抓取所有信息，暂停状态的迭代也会同步，但抓取的信息有所删选，只抓取在迭代发布之后需要关注的数据。

#### 数据收集与分析

按照迭代管理中的配置，从对应服务器抓取数据，经过初次整理后存入数据库，二次分析后产生更多的指标数据。

#### 看板

展示数据整理分析之后的图表和信息，用以辅助关注者进行软件质量情况的评判。

# 安装部署

#### 安装部署

```bash
docker-compose -f docker-compose.yaml pull
docker-compose -f docker-compose.yaml up -d
```

#### 升级

> 同安装

```bash
docker-compose -f docker-compose.yaml pull
docker-compose -f docker-compose.yaml up -d
```

# 使用方法

#### 快速开始

# Q&A

#### Q: 项目/迭代的激活/暂停是什么意思？

> A: 激活代表迭代进行中，发布后建议手动设置为暂停，不再需要对研发过程进行数据抓取，激活状态抓取的数据更全更多。
