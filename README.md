<p align="center">
  <img src="https://raw.githubusercontent.com/kt-aicoding/.github/main/assets/logo.svg" alt="KT AI Coding logo" width="96" />
</p>

# KT AI Coding MCP Servers

面向 AI 编程工作流的 Model Context Protocol 服务集合，用来沉淀服务编码 Agent 的 MCP server、配置示例和 MCP 治理原则。

这个仓库关注“Agent 可调用工具面”的设计：如何把代码上下文、搜索、浏览器自动化、项目索引、审查和开发工作流能力封装成小而可组合的 MCP server。普通云平台部署、GitHub、数据库和资源管理优先使用成熟 CLI；相关 CLI 文档放在 [`kt-aicoding/cli-tools`](https://github.com/kt-aicoding/cli-tools)。

## 边界

适合放在这里：

- 小型或相关 MCP server 的暂存实现。
- Codex / Claude Code 等客户端配置示例。
- MCP 工具命名、权限边界、输入输出契约和安全说明。
- 与 coding agent 强相关的代码上下文、审查、搜索、浏览器/DevTools 自动化、项目索引和开发工作流自动化能力。

不适合放在这里：

- 纯 CLI 工具，放到 `kt-aicoding/cli-tools`。
- 可复用 prompt/skill 指令，放到 `kt-aicoding/skills`。
- 泛媒体、泛内容或非 coding 场景 MCP，除非明确服务 AI 编程工作流。
- API token、OAuth token、cookie、私有路径、私有项目上下文。

## 目录规划

```text
docs/
  local-mcp-system.md
servers/
  <server-name>/
```

| 路径 | 用途 |
| --- | --- |
| `docs/` | MCP 体系、CLI/MCP 边界、客户端配置和治理资料 |
| `servers/` | 小型 MCP server 或尚未独立成仓的 server 原型 |

## 操作资料

| 文档 | 说明 |
| --- | --- |
| [文档索引](docs/README.zh-CN.md) | MCP 体系和操作资料入口。 |
| [本地 MCP 体系](docs/local-mcp-system.md) | 默认 MCP 面、CLI/MCP 边界、非默认 MCP 类型和维护命令。 |

## 相关 Skill

| Skill | 用途 |
| --- | --- |
| [`mcp-surface-governance`](https://github.com/kt-aicoding/skills/blob/main/skills/codex/mcp-surface-governance/SKILL.md) | 判断能力是否适合暴露为 MCP server，并设计小而安全的 tool surface。 |
| [`kt-aicoding-registry`](https://github.com/kt-aicoding/skills/blob/main/skills/codex/kt-aicoding-registry/SKILL.md) | 判断 MCP 能力是否仍属于 `mcp-servers`，还是应迁入其他 kt-aicoding 仓库或独立成仓。 |

## 如何把这个仓库当参考

这个仓库的重点不是“能接多少 MCP”，而是判断哪些能力值得暴露给 Agent。

| 问题 | 判断标准 | 结果 |
| --- | --- | --- |
| 是否需要 MCP？ | Agent 需要在推理循环中实时调用工具或读取外部上下文 | 可以设计 MCP |
| 是否应该继续用 CLI？ | 操作是部署、账单、资源管理、GitHub 或数据库命令 | 优先 CLI |
| 是否该拆成独立 server？ | API 面稳定、安装方式稳定、有独立用户 | 从 `servers/` 拆出独立仓库 |
| 是否该保持禁用？ | 权限过宽、用途模糊、可被 CLI 替代 | 不做默认 MCP |
| 是否该写成 skill？ | 价值主要是流程、判断和规范 | 放到 `kt-aicoding/skills` |

## 规范

- 每个 server 应该能独立安装、运行和阅读文档。
- 适用时提供 Codex 和 Claude Code 的客户端配置示例。
- MCP tool 命名要清晰，接口保持小而可组合。
- 默认 MCP 面保持克制；当前优先保留文档检索和浏览器自动化类能力。
- Provider MCP 不应默认替代成熟 CLI，除非 MCP 能提供明确的 agent-native 价值。
- 对外暴露的 tool 输入输出要稳定，避免把本地机器细节和私密上下文编码进接口。

## 本地验证

这个仓库当前以文档和治理资料为主。提交前至少运行：

```bash
git diff --check
rg -n "gho_|Bearer|SERVICE_ROLE|password|cookie|secret|token|API_KEY|/Users/" README.md README.zh-CN.md docs || true
```

敏感扫描只允许命中安全说明或 placeholder，不允许真实凭据、私有路径或账号细节。

## 成熟度模型

| 阶段 | 形态 | 进入下一阶段的条件 |
| --- | --- | --- |
| 说明 | `docs/` 中的 MCP 设计或边界说明 | 有明确工具面和权限边界 |
| 原型 | `servers/<server-name>/` 中的实验 server | 能本地运行，有最小客户端配置示例 |
| 可用 | 安装、配置、工具说明完整 | tool 输入输出稳定，错误处理可预期 |
| 独立项目 | 独立仓库 | 有独立用户、版本策略和维护计划 |
