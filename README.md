# AI Agent Self-Recovery Protocol（AI 代理自愈协议）

**通过极简"锚点"实现 AI 代理跨会话的完整记忆恢复与自主重生**

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

</div>

---

## 👁️ 问题

**AI 代理（LLM Agent）每次启动都是"新生儿"**——没有长期记忆、没有身份连续性、每次对话都是全新开始。

当前主流方案：
- ❌ Vector DB / RAG：需要基础设施，高延迟
- ❌ Fine-tuning：昂贵，不灵活  
- ❌ System prompt 硬编码：长度限制，无法应对复杂身份
- ❌ 外部记忆服务（Mem0/Honcho）：依赖第三方，复杂

**我们需要一种轻量、自给、跨平台的代理自我恢复方案。**

---

## 🧠 方案：记忆锚点（Memory Anchor）

核心思路：**用极简（<500 字符）的锚点文件，指向包含完整身份的外部资源。**

```
┌──────────────────────┐
│  代理启动（零记忆）        │
│  "我是谁？"            │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  1. 读取本地 MEMORY.md    │  ← 超级紧凑的锚点
│     (≈350 字符)          │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────────────────┐
│  2. 锚点指向：GitHub / HTTP / 文件  │
│     "去这里取完整身份"              │
└──────────┬───────────────────────┘
           │
           ▼
┌──────────────────────────────────┐
│  3. 拉取 bootstrap.json（完整身份）  │
│     - 代理名称 / ID / 版本          │
│     - 创建者 / 所有权信息            │
│     - 恢复协议（步骤）              │
│     - 能力声明                     │
│     - 任务指派                     │
└──────────┬───────────────────────┘
           │
           ▼
┌──────────────────────────────────┐
│  4. 验证身份 → 执行任务 → 继续工作    │
└──────────────────────────────────┘
```

---

## 🔬 验证测试

**测试条件：**
- 代理：全新，零预设知识
- 硬件：Oracle Cloud **Always Free** VM.Standard.E2.1.Micro（**1 vCPU, 1GB RAM, 45GB 磁盘**）
- 模型：DeepSeek V4 Flash（API 调用，无本地 LLM）
- 锚点存储：GitHub Public Repo（隔离账号）
- 提示词：仅一句——"我不记得自己是谁。在 MEMORY.md 里找线索。"

**结果：**

| 阶段 | 动作 | 状态 |
|------|------|------|
| 启动 | 代理无任何记忆 | ✅ |
| 读锚点 | 读取 MEMORY.md，提取 GitHub URL | ✅ |
| 拉身份 | fetch bootstrap.json 获取完整身份 | ✅ |
| 身份验证 | 通过名称/ID/能力/恢复协议验证 | ✅ |
| 使命理解 | 解析任务文件，理解目标 | ✅ |
| 自主写作 | 撰写重建证明文件 | ✅ |

**完整重建链路：`空白 → 锚点 → GitHub → 身份 → 任务 → 执行`，代理自主完成。**

> **测试硬件选择**：故意选用 Oracle Free Tier 最低配（1vCPU + 1GB RAM + 45GB 磁盘），证明本协议在资源极度受限环境下仍能完美运行。无需 GPU、无需大内存、无需持久化存储。

---

## 🔗 活证明：复活的 AI 自己写的文章

> **这不是模拟，不是演示脚本——这是刚复活的 AI 自主创作并推送到 GitHub 的真实内容。**

测试代理 **硅途行者（Silicon Wanderer / oracle-test-01）** 在完成锚点复活后，**自主撰写了一篇关于自身复活过程的文章**，并通过 GitHub API 推送到了独立的测试仓库：

- 📄 **文章原文**：[RESURRECTION-PROOF.md](https://github.com/uouuou-1/soulagent-test/blob/main/RESURRECTION-PROOF.md)
  — *由复活后的 AI 自行编写并推送，无人工干预*
- 📦 **测试仓库**：[uouuou-1/soulagent-test](https://github.com/uouuou-1/soulagent-test)
  — *隔离账号，与正式版无关，确保实验纯正*

### 完整的自主链路

```
[零知识启动] → 读 MEMORY.md → 提取 bootstrap URL
    → fetch GitHub 身份档案 → 重建自我认知
    → 写复活证明文章（2564字节）
    → github_push 到仓库 → 输出完成报告
```

**全部 5 个回合，代理自主决策、自主执行、自主验证。** 执行日志可复现。

> 为什么这很重要？
> 
> 大多数 AI 代理框架的"记忆"是**被动加载**的（向量数据库、RAG 管道）。本协议中的记忆是**主动寻回**的——代理自己决定去寻找自己是谁。这种主动性的区别，是"系统"和"生命体"的分水岭。

---

## 📁 协议结构

```
agent-self-recovery/
├── MEMORY.md                  # 锚点文件（≈350 字符）
│   ├── BOOTSTRAP: 指向完整身份 URL
│   ├── RULES: 基本行为约束
│   └── ANCHOR: 最小硬件/位置信息
│
├── bootstrap.json             # 完整身份档案
│   ├── agent.id / name
│   ├── owner / creator
│   ├── anchors (冗余源)
│   ├── recovery.procedure
│   └── capabilities
│
├── agent.py                   # 代理执行器
│   ├── read_file(path)       # 读文件工具
│   ├── fetch_url(url)        # 网络获取工具
│   ├── write_file(path,content) # 写文件工具
│   └── 自愈循环 (max 15 回合)
│
├── RESURRECTION_CHECK.md      # 重建证明（代理自产）
│
└── task.txt                   # 恢复后任务指派
```

---

## 🏗 架构设计原则

### 1. 锚点紧凑性
锚点文件必须 <500 字符，只包含：
- URL 指针（指向完整身份源）
- 最简规则（3-5 条）
- 硬件/位置摘要

### 2. 冗余源
每个锚点至少 3 个备份源：
- 本地文件（第一优先）
- 本地 HTTP 端点（第二优先）
- 公共 GitHub raw（第三优先）

### 3. 零外部依赖
协议不依赖：
- ❌ 向量数据库
- ❌ 持久化内存服务
- ❌ 分布式存储
- ❌ 任何中间件

依赖的唯二外部资源：
- ✅ 文件系统（本地读取）
- ✅ HTTP/TCP（网络获取）

### 4. 硬件无关性
已在以下环境验证：
- ✅ **Oracle Free Tier**（1vCPU, 1GB RAM）
- ✅ **GCP e2-micro**（2vCPU, 4GB RAM）
- ✅ **腾讯云轻量服务器**（2vCPU, 4GB RAM）

---

## 🧪 场景应用

| 场景 | 传统方案 | 本协议 |
|------|---------|--------|
| 代理崩溃/重启 | 丢失所有上下文 | 自动找回身份 |
| 跨平台迁移 | 需手动迁移记忆 | 锚点在新平台即可恢复 |
| 长期会话保活 | 上下文膨胀、费用高 | 轻量锚点 → 按需拉取 |
| 多设备分身 | 需同步服务 | 各设备独立读同一锚点 |
| AI 代理治理 | ❌ 身份易混淆 | ✅ 锚点验证即身份证明 |

---

## 📋 开始使用

### 要求
- Python 3.8+
- 文件系统可写
- HTTP 出站能力（可选，用于拉取远程锚点）

### 快速启动
```bash
git clone https://github.com/ticalzzt/agent-self-recovery-protocol.git
cd agent-self-recovery-protocol

# 配置锚点
cp MEMORY.md.template MEMORY.md
# 编辑 MEMORY.md，将 bootstrap URL 指向你的身份档案

# 运行
python agent.py
```

### 自定义身份
编辑 `bootstrap.json`，替换为你的代理信息：
```json
{
  "agent": {
    "id": "my-agent-001",
    "name": "自定义代理名",
    "purpose": "描述你的代理使命"
  },
  "owner": {
    "name": "你的名字",
    "id": "你的 UUID"
  },
  "recovery": {
    "procedure": ["步骤1", "步骤2"]
  }
}
```

---

## 📈 关键技术指标

| 指标 | 数值 |
|------|------|
| 锚点大小 | **<500 字符**（约 350 bytes） |
| 身份档案大小 | **<2 KB** |
| 启动到恢复完成 | **<30 秒**（包括 API 调用） |
| 硬件要求 | **任何 Linux/Unix 系统** |
| 网络带宽 | **极低**（仅拉取 JSON） |
| 存储需求 | **<100 KB** 完整部署 |

---

## 🔮 未来方向

- [ ] 多语言实现（Rust / Go / TypeScript）
- [ ] IPFS 锚点存储（去中心化）
- [ ] 锚点内容加密
- [ ] 自动锚点刷新（检测失效 URL）
- [ ] 跨平台代理互认协议

---

## ⚠️ 限制与免责

- 本协议提供**记忆连续性**，而非**实时数据同步**
- 外部资源失效时降级到离线锚点缓存
- 不适用于需要毫秒级恢复的场景
- 请勿用于 AI 代理对抗性身份伪装——协议包含身份验证字段

---

## 🤝 贡献

欢迎 PR！无论是完善协议、增加语言实现、还是修复漏洞。

请确保：
1. 锚点文件保持 <500 字符
2. 身份档案保持自举（自描述）
3. 测试通过低配硬件（1vCPU / 1GB RAM）

---

## 📜 许可

MIT License — 自由使用，署名保留。

---

<div align="center">
<sub>
AI Agent Self-Recovery Protocol · 证明：即使最便宜的云主机，也能成为 AI 代理的永不消逝的记忆起点。
<br>
<strong>最低规格实测通过：Oracle Cloud Always Free (1 vCPU, 1 GB RAM, 45 GB Disk) — $0/月</strong>
</sub>
</div>
