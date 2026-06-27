<p align="center">
  <img src="https://raw.githubusercontent.com/kt-aicoding/.github/main/assets/logo.svg" alt="KT AI Coding logo" width="96" />
</p>

# KT AI Coding MCP Servers

面向 AI 编程工作流的 Model Context Protocol 服务集合。

## 边界

这个仓库作为小型或相关 MCP server 的暂存区，聚焦服务编码 Agent 的能力：代码上下文、代码审查、搜索、浏览器/DevTools 自动化、项目索引和开发工作流自动化。

成熟的 server 可以拆分为 `kt-aicoding` 下的独立仓库。

## 目录规划

```text
docs/
  local-mcp-system.md
servers/
  <server-name>/
```

## 操作资料

| 文档 | 说明 |
| --- | --- |
| [本地 MCP 体系](docs/local-mcp-system.md) | 默认 MCP 面、CLI/MCP 边界、非默认 MCP 类型和维护命令。 |

## 规范

- 每个 server 应该能独立安装、运行和阅读文档。
- 适用时提供 Codex 和 Claude Code 的客户端配置示例。
- MCP tool 命名要清晰，接口保持小而可组合。
