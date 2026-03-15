# creating-mermaid-diagrams

Claude Code 技能：生成 Mermaid 图表并本地导出为 PNG/SVG/PDF。

[English](README.md)

## 为什么选择这个技能？

| 特性 | 本技能 | 其他 Mermaid 技能 | MCP 服务器 |
|------|--------|------------------|------------|
| **导出前验证** | ✓ 必须步骤 | 经常跳过 | 不一定 |
| **渐进式加载** | ✓ 语法分离到独立文件 | 全部内联 | 不适用 |
| **主动触发** | ✓ 3+组件自动触发 | 仅手动 | 仅手动 |
| **中文支持** | ✓ 画图、架构图、流程图、时序图 | 仅英文 | 仅英文 |
| **输入输出示例** | ✓ 3个完整示例 | 通常没有 | 没有 |
| **本地导出** | ✓ 通过 mmdc 导出 PNG/SVG/PDF | 通常基于网页 | 网页预览 |
| **无 API 依赖** | ✓ 完全离线 | 部分需要 API | 通常需要 API |

**核心优势：**
- **提前捕获错误** — 验证循环防止生成损坏的图表
- **Token 高效** — 详细语法仅在需要时加载
- **离线工作** — 无需外部服务
- **双语支持** — 中英文关键词都能触发

## 这个技能能做什么

### 图表类型（11+种）

| 类型 | 用途 | 示例 |
|------|------|------|
| **流程图** | 流程、管道、决策树 | CI/CD 管道、用户注册流程 |
| **时序图** | API 调用、认证流程 | JWT 认证、微服务通信 |
| **类图** | OOP 模型、数据结构 | 领域模型、继承层次 |
| **ER 图** | 数据库 Schema | 用户-订单-商品关系 |
| **状态图** | 状态机、生命周期 | 订单状态、连接状态 |
| **甘特图** | 项目时间线 | Sprint 规划、发布计划 |
| **饼图** | 比例、分布 | 市场份额、资源分配 |
| **Git 图** | 分支策略 | GitFlow、主干开发 |
| **C4 上下文图** | 高级架构 | 系统上下文、容器图 |
| **思维导图** | 主题分解 | 功能规划、头脑风暴 |

### 输出格式

- **PNG** — 高分辨率（2048px），白色背景，多种主题
- **SVG** — 可缩放矢量图，适合文档
- **PDF** — 可打印文档

### 自动触发

技能在以下情况自动激活：
- 明确请求图表：*"创建流程图"*、*"画架构图"*
- 解释复杂系统：*"认证是怎么工作的"*（3+组件）
- 使用中文：*"画一个时序图"*、*"架构图"*

## 如何使用这个技能

### 1. 安装技能

```bash
# 克隆到 Claude Code 技能目录
git clone https://github.com/Agents365-ai/creating-mermaid-diagrams.git ~/.claude/skills/creating-mermaid-diagrams
```

或者用于特定项目：
```bash
git clone https://github.com/Agents365-ai/creating-mermaid-diagrams.git .claude/skills/creating-mermaid-diagrams
```

### 2. 安装依赖

```bash
# 安装 Mermaid CLI
npm install -g @mermaid-js/mermaid-cli

# 验证安装
mmdc --version
```

如果 Chromium 下载失败：
```bash
PUPPETEER_SKIP_DOWNLOAD=true npm install -g @mermaid-js/mermaid-cli
```

### 3. 开始使用

在 Claude Code 中描述你想要的：

```
创建一个用户认证的时序图，使用 JWT
```

```
画一个电商微服务架构图
```

```
Draw an e-commerce microservices architecture
```

Claude 会：
1. 生成 `.mmd` 源文件
2. **验证语法**（在导出前捕获错误）
3. 导出为 PNG/SVG/PDF
4. 报告输出文件路径

## 示例输出

**提示词：**
> 创建一个微服务电商架构，包含 API 网关、各种服务和数据库

**生成结果：**

![微服务架构](assets/example.png)

## 文件结构

```
creating-mermaid-diagrams/
├── SKILL.md              # 主技能说明
├── reference/
│   ├── FLOWCHART.md      # 流程图语法和示例
│   ├── SEQUENCE.md       # 时序图语法
│   ├── CLASS-ER.md       # 类图和 ER 图语法
│   └── OTHER-TYPES.md    # 状态图、甘特图、Git图、饼图、思维导图、C4
├── assets/
│   └── example.png
├── README.md
└── README_CN.md
```

## 许可证

MIT

## 作者

**Agents365-ai**

- GitHub: https://github.com/Agents365-ai
- Bilibili: https://space.bilibili.com/441831884
