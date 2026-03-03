# mermaid-skill

用于在 Claude Code 中生成 Mermaid 图表并本地导出为 PNG/SVG/PDF 的 skill。

[English](README.md)

## 功能说明

- 根据自然语言描述生成 `.mmd` 文本文件
- 使用 `mmdc` CLI（Mermaid CLI）将图表导出为 PNG、SVG 或 PDF
- 支持 10+ 种图表类型：流程图、时序图、类图、ER 图、状态图、甘特图、饼图、Git 图、C4 架构图、思维导图
- **无需手动定位** — 布局完全自动，无需指定坐标
- 当图表有助于解释复杂系统时自动触发

## 依赖项

| 工具 | 用途 |
|------|------|
| `mmdc`（`@mermaid-js/mermaid-cli`）| CLI，用于将 `.mmd` 导出为 PNG/SVG/PDF |

需要 Node.js 和 npm。

## 安装

### macOS / Windows / Linux

```bash
# 全局安装 mmdc
npm install -g @mermaid-js/mermaid-cli

# 验证安装
mmdc --version
```

如果 Chromium 下载失败：
```bash
PUPPETEER_SKIP_DOWNLOAD=true npm install -g @mermaid-js/mermaid-cli
```

### 平台说明

| 平台 | 额外步骤 |
|------|----------|
| **macOS** | npm 安装后无需额外操作 |
| **Windows** | npm 安装后无需额外操作 |
| **Linux** | 无需额外操作（mmdc 内部处理无头 Chromium）|

## 使用方式

直接描述你想要的图表：

```
画一个微服务电商架构图，包含 API Gateway，用户/订单/商品/支付服务，
Kafka 事件总线，通知服务，以及各自独立的数据库
```

Claude 会自动生成 `.mmd` 文件并导出为 PNG。

## 示例

**提示词：**
> 画一个微服务电商架构图，包含 Mobile/Web/Admin 客户端，API Gateway，
> 用户/订单/商品/支付服务，Kafka 事件总线，通知服务，
> 以及 User DB / Order DB / Product DB / Redis Cache / Stripe API

**输出效果：**

![微服务架构图](assets/example.png)

## 图表类型

| 类型 | 关键词 | 适用场景 |
|------|--------|----------|
| 流程图（从上到下） | `flowchart TD` | 流程、决策树、数据管道 |
| 流程图（从左到右） | `flowchart LR` | 数据流、横向管道 |
| 时序图 | `sequenceDiagram` | API 调用、协议流、消息传递 |
| 类图 | `classDiagram` | OOP 模型、数据结构 |
| ER 图 | `erDiagram` | 数据库 Schema |
| 状态图 | `stateDiagram-v2` | 状态机、生命周期 |
| 甘特图 | `gantt` | 项目时间线 |
| 饼图 | `pie` | 比例分布 |
| Git 图 | `gitGraph` | 分支策略 |
| C4 架构图 | `C4Context` | 高层架构概览 |
| 思维导图 | `mindmap` | 主题拆解 |

## 文件说明

- `SKILL.md` — Claude Code 加载的 skill 指令文件
- `README.md` — 英文说明
- `README_CN.md` — 本文件（中文）
- `assets/` — 示例图表

## 开源协议

MIT

## 支持作者

如果这个 skill 对你有帮助，欢迎支持作者：

<table>
  <tr>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/wechat-pay.png" width="180" alt="微信支付">
      <br>
      <b>微信支付</b>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/alipay.png" width="180" alt="支付宝">
      <br>
      <b>支付宝</b>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/buymeacoffee.png" width="180" alt="Buy Me a Coffee">
      <br>
      <b>Buy Me a Coffee</b>
    </td>
  </tr>
</table>

## 作者

**Agents365-ai**

- Bilibili: https://space.bilibili.com/441831884
- GitHub: https://github.com/Agents365-ai
