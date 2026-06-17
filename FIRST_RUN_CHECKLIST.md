# 首次启动检查清单

使用本模板创建新项目或新会话前，确认以下事项。

## 必须为空

- `state/project-board.md` 只保留表头，没有真实需求。
- `state/decision-log.md` 只保留表头，没有真实决策。
- `inbox/request-template.md` 只保留模板内容，没有真实需求。
- `docs/tasks/` 只保留模板和 README。
- `docs/requirements/` 只保留模板和 README。
- `docs/api/` 只保留模板和 README。
- `docs/testing/` 只保留模板和 README。
- `docs/reports/` 只保留模板和 README。

## 必须存在

- `START_HERE.md`
- `AGENTS.md`
- `agent-manifest.yaml`
- `agents/shared-rules.md`
- `docs/architecture/TECH_STACK.md`
- `docs/process/CONTINUOUS_DELIVERY_RULES.md`
- `prompts/single-window-start.md`
- `prompts/multi-window-start.md`

## 启动方式

单窗口模式：

```text
请读取 prompts/single-window-start.md，并按其中规则工作。
```

多窗口模式：

```text
请读取 prompts/multi-window-start.md，并按其中规则为每个角色窗口启动。
```

## 首次需求

首次需求应由项目经理 Agent 接收。不要直接把原始需求交给前端、后端或测试 Agent。

