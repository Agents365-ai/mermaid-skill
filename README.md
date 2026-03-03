# mermaid-skill

Claude Code skill for generating Mermaid diagrams and exporting to PNG/SVG/PDF locally.

[中文文档](README_CN.md)

## What it does

- Generates `.mmd` text files from natural language descriptions
- Exports diagrams to PNG, SVG, or PDF using the `mmdc` CLI (Mermaid CLI)
- Supports 10+ diagram types: flowchart, sequence, class, ER, state, Gantt, pie, gitGraph, C4, mindmap
- **No manual positioning** — layout is fully automatic
- Triggers automatically when diagrams would help explain complex systems

## Dependencies

| Tool | Purpose |
|------|---------|
| `mmdc` (`@mermaid-js/mermaid-cli`) | CLI to export `.mmd` → PNG/SVG/PDF |

Requires Node.js and npm.

## Install

### macOS / Windows / Linux

```bash
# Install mmdc globally
npm install -g @mermaid-js/mermaid-cli

# Verify
mmdc --version
```

If Chromium download fails:
```bash
PUPPETEER_SKIP_DOWNLOAD=true npm install -g @mermaid-js/mermaid-cli
```

### Platform notes

| Platform | Extra step |
|----------|------------|
| **macOS** | No extra steps after npm install |
| **Windows** | No extra steps after npm install |
| **Linux** | No extra steps (mmdc handles headless Chromium internally) |

## Usage

Just describe what you want:

```
Create a microservices e-commerce architecture with API Gateway, user/order/product/payment services,
Kafka event bus, notification service, and separate databases for each service
```

Claude will generate the `.mmd` file and export it to PNG automatically.

## Example

**Prompt:**
> Create a microservices e-commerce architecture with Mobile/Web/Admin clients, API Gateway,
> User/Order/Product/Payment services, Kafka Event Bus, Notification service,
> and User DB / Order DB / Product DB / Redis Cache / Stripe API

**Output:**

![Microservices Architecture](assets/example.png)

## Diagram Types

| Type | Keyword | Use for |
|------|---------|---------|
| Flowchart | `flowchart TD` / `flowchart LR` | processes, decision trees, pipelines |
| Sequence | `sequenceDiagram` | API calls, protocol flows, message passing |
| Class | `classDiagram` | OOP models, data structures |
| ER | `erDiagram` | database schemas |
| State | `stateDiagram-v2` | state machines, lifecycle |
| Gantt | `gantt` | project timelines |
| Pie | `pie` | proportions, distributions |
| Git Graph | `gitGraph` | branch strategies |
| C4 Context | `C4Context` | high-level architecture |
| Mind Map | `mindmap` | topic breakdowns |

## Files

- `SKILL.md` — skill instructions loaded by Claude Code
- `README.md` — this file (English)
- `README_CN.md` — Chinese documentation
- `assets/` — example diagrams

## License

MIT

## Support

If this skill helps you, consider supporting the author:

<table>
  <tr>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/wechat-pay.png" width="180" alt="WeChat Pay">
      <br>
      <b>WeChat Pay</b>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/alipay.png" width="180" alt="Alipay">
      <br>
      <b>Alipay</b>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/Agents365-ai/images_payment/main/qrcode/buymeacoffee.png" width="180" alt="Buy Me a Coffee">
      <br>
      <b>Buy Me a Coffee</b>
    </td>
  </tr>
</table>

## Author

**Agents365-ai**

- Bilibili: https://space.bilibili.com/441831884
- GitHub: https://github.com/Agents365-ai
