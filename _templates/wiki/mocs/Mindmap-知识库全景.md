---
title: "知识库全景思维导图"
type: moc
aliases: ["知识库思维导图", "vault mindmap"]
tags: [思维导图, MOC, mermaid, 时序图]
sources: []
created: 2026-08-15
last_updated: 2026-09-13
status: finished
---

# 知识库全景

> [!tip] 关于本页面
> 本页所有图表使用 **Mermaid** 语法，Obsidian 原生支持，无需安装任何插件。
> 图表配色由 `wiki-mermaid.css` 统一接管：**同一份源码在深色与浅色主题下都能正确显示**，
> 因此这里不使用 `style X fill:#...` 这类硬编码颜色，而是通过语义 `class` 引用配色变量。

## 架构总览

```mermaid
mindmap
  root((LLM Wiki))
    原始资料 raw
      文章 01-articles
      论文 02-papers
      转录 03-transcripts
      笔记 04-meeting_notes
      归档 09-archive
    知识编译 wiki
      概念 concepts
        框架
        方法论
        理论
      实体 entities
        人物
        公司
        工具
        产品
      来源摘要 sources
        可信度评估
      综合分析 syntheses
        跨源对比
      主题地图 mocs
        MOC技术
        MOC商业
        MOC人物
        MOC待整理
    媒体资源 assets
      图片
      PDF
      附件
    Agent 技能
      ingest 摄入
        增量编译
        讨论确认
        URL 摄入
      query 查询
      lint 健康检查
        死链检测
        概念空缺
        研究建议
      refresh 联网刷新
        按领域周期
        冲突标记
      canvas 可视化
    配置体系
      Obsidian 配置
        app.json
        appearance.json
        templates.json
        graph.json
      CSS 样式
        wiki-reading
        wiki-callouts
        wiki-components
        wiki-mermaid
        wiki-markmap
        wiki-canvas
      模板系统
        entity
        concept
        source
        synthesis
```

## 知识摄入时序

展示一次 `/ingest` 从增量检测到归档的完整往返过程。

```mermaid
sequenceDiagram
    autonumber
    participant U as 👤 用户
    participant A as 🤖 ingest
    participant R as 📥 raw/
    participant W as 🧠 wiki/
    participant S as 💾 state.json

    Note over U,S: 阶段一 · 增量检测
    U->>A: /ingest raw/01-articles
    A->>S: 读取处理记录
    S-->>A: 返回已完成哈希
    A->>A: 比对文件哈希

    alt 文件未处理
        Note over A,W: 阶段二 · 知识编译
        A->>R: 读取源文件
        R-->>A: 返回正文
        A->>U: 展示提取的实体与概念
        U-->>A: 确认 / 修正
        activate A
        A->>W: 创建来源摘要
        A->>W: 创建或更新概念页
        A->>W: 创建或更新实体页
        deactivate A
        loop 每个提取出的概念
            A->>W: 增量合并双链
        end
    else 已处理过
        A-->>U: 跳过（内容无变更）
    end

    A->>S: 写入处理状态
    A->>R: 归档至 09-archive/
    A-->>U: ✅ 输出编译完成报告
```

## 知识编译流程

```mermaid
flowchart LR
    subgraph Raw["📥 raw/ 不可变层"]
        R1[文章]
        R2[论文]
        R3[转录]
        R4[URL 网页]
    end

    subgraph Ingest["🤖 ingest"]
        I1[提取实体概念]
        I2[讨论确认]
        I3[创建 wiki 页面]
    end

    subgraph Wiki["🧠 wiki/ 编译层"]
        W1[concepts/]
        W2[entities/]
        W3[sources/]
        W4[syntheses/]
        W5[index.md]
    end

    subgraph Maintain["🔧 维护"]
        M1[lint 健康检查]
        M2[refresh 联网更新]
        M3[canvas 可视化]
    end

    R1 & R2 & R3 --> I1
    R4 -->|自动抓取| I1
    I1 --> I2 --> I3
    I3 --> W1 & W2 & W3 & W4
    I3 --> W5

    W1 & W2 & W3 & W4 --> M1
    W1 & W2 & W3 & W4 --> M2
    W1 & W2 & W3 & W4 --> M3

    class R1,R2,R3,R4 red
    class I1,I2,I3 green
    class W1,W2,W3,W4,W5 cyan
    class M1,M2,M3 purple

```

## Agent 技能交互

```mermaid
flowchart TD
    User(["👤 用户"])

    User -->|"/ingest path"| IG["🤖 ingest<br/>增量编译"]
    User -->|"/ingest url"| IG
    User -->|"/query 问题"| QY["🔍 query<br/>智能查询"]
    User -->|"/lint"| LT["🩺 lint<br/>健康检查"]
    User -->|"/refresh"| RF["🔄 refresh<br/>联网更新"]
    User -->|"/canvas"| CV["🎨 canvas<br/>图谱生成"]

    IG -->|写入| Wiki[("🧠 wiki/")]
    QY -->|读取| Wiki
    LT -->|扫描| Wiki
    RF -->|更新| Wiki
    CV -->|读取| Wiki

    IG -.->|遵循规范| OM["📐 obsidian-markdown<br/>语法规范"]
    QY -.-> OM
    LT -.-> OM
    RF -.-> OM

    IG -->|状态追踪| IS[("💾 ingest-state")]
    RF -->|状态追踪| RS[("💾 refresh-state")]

    LT -->|输出| Report["健康报告<br/>死链 / 孤儿 / 空缺"]
    QY -->|输出| Answer["回答<br/>带 wikilink 来源"]
    RF -->|输出| Refreshed["刷新报告<br/>更新 / 冲突"]
    CV -->|输出| Canvas[".canvas 文件"]

    class User solid
    class Wiki cyan
    class IS,RS,Refreshed orange
    class OM purple

```

## 目录权限模型

三层分离架构：不可变层 → 媒体层 → 编译层。

```mermaid
flowchart TB
    subgraph Immutable["⛔ 不可变层"]
        direction LR
        RAW["raw/<br/>原始资料<br/>只读"]
        ARC["raw/09-archive/<br/>归档区<br/>禁止读取"]
    end

    subgraph Media["🖼️ 媒体层"]
        ASSETS["assets/<br/>图片 / PDF / 附件<br/>引用 ![[file]]"]
    end

    subgraph Workspace["✏️ 编译层 Agent 工作区"]
        direction LR
        WIKI["wiki/<br/>概念 / 实体 / 来源 / 综合<br/>可创建 / 更新 / 提炼"]
        TPL["templates/<br/>Templater 模板<br/>只读引用"]
    end

    subgraph Config["⚙️ 配置层"]
        direction LR
        OBS[".obsidian/<br/>Obsidian 配置"]
        CLD[".claude/<br/>Agent Skills + 状态文件"]
    end

    RAW -->|ingest 编译| WIKI
    WIKI -->|![[嵌入]]| ASSETS
    TPL -.->|模板引用| WIKI

    class RAW,ARC red
    class ASSETS orange
    class WIKI green
    class TPL,CLD blue
    class OBS purple

```

## 关联连接

- [[index]] — 全局内容字典
- [[log]] — 操作日志
- [[MOC-技术]] — 技术领域主题地图
- [[MOC-商业]] — 商业领域主题地图
- [[MOC-人物]] — 人物与机构主题地图
- [[MOC-待整理]] — 待分类与草稿
