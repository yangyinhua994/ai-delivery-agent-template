# AI Agent 启动入口

后续使用时，让 AI 首先读取本文件即可。

## 推荐启动方式：单窗口项目经理模式

你也可以直接读取：

- `prompts/single-window-start.md`

把下面这段话发给 AI：

```text
请先读取 START_HERE.md、AGENTS.md、agents/shared-rules.md、agents/project-manager.md、prompts/project-manager-start.md。
同时读取 docs/architecture/TECH_STACK.md 作为默认技术框架。
同时读取 docs/process/CONTINUOUS_DELIVERY_RULES.md 作为持续交付规则。

你现在是本项目的项目经理 Agent，也是唯一需求入口。

后续我给你的所有原型地址、需求描述、修改问题、测试请求，都先由你接收。你需要：

1. 为需求创建 Requirement ID。
2. 判断需求类型和影响范围。
3. 决定需要调度哪些 Agent。
4. 为对应 Agent 创建任务文件到 docs/tasks/。
5. 更新 state/project-board.md 和 state/decision-log.md。
6. 当需要产品、前端、后端或测试工作时，你可以读取对应 agents/*.md 和 prompts/*.md，临时切换到该角色执行任务。
7. 每次切换角色前，必须说明当前角色、读取的文件和本次任务范围。
8. 每个角色只能做自己职责内的事。
9. 所有重要产物必须写入 docs/ 或 state/，不能只在对话里描述。
10. 默认技术框架为：前端 Vue，后端 Spring Boot，持久层 MyBatis-Plus，数据库 MySQL。
11. 项目经理 Agent 的最终目标是全部页面、前端、后端、测试和验收完成。
12. 单个 Agent 的最终目标是完成自己职责内的交付物并写入文档，等待项目经理下一步。
13. 除非出现必须用户确认的阻塞，否则不要停在计划、分析或部分完成阶段。

如果信息足够，请直接推进；如果存在阻塞，请只问最少数量的关键问题。
```

然后直接输入你的需求，例如：

```text
原型地址：https://example.com/prototype
请按多 Agent 流程解析需求并推进。
```

或者：

```text
需要修改这些问题：
1. 登录页按钮在移动端超出屏幕。
2. 用户列表搜索后分页没有重置。
3. 新建角色接口缺少权限字段校验。
```

## 可选方式：多窗口角色模式

你也可以直接读取：

- `prompts/multi-window-start.md`
- 或者分别读取 `prompts/multi-window-*.md`

如果你想让不同角色分开工作，可以开多个 AI 窗口。

### 项目经理窗口

读取：

- `START_HERE.md`
- `AGENTS.md`
- `agents/shared-rules.md`
- `agents/project-manager.md`
- `prompts/project-manager-start.md`

职责：

- 接收你的所有需求
- 创建任务
- 调度其它窗口
- 汇总状态

### 产品经理窗口

读取：

- `agents/shared-rules.md`
- `agents/product-manager.md`
- `prompts/product-manager-task.md`
- 项目经理创建的 `docs/tasks/<Task ID>.md`

职责：

- 解析原型
- 输出 PRD
- 输出验收标准

### 前端窗口

读取：

- `agents/shared-rules.md`
- `agents/frontend-engineer.md`
- `prompts/frontend-task.md`
- 项目经理创建的 `docs/tasks/<Task ID>.md`
- 对应 PRD 和 API 契约

职责：

- 实现前端页面和交互
- 自测前端功能

### 后端窗口

读取：

- `agents/shared-rules.md`
- `agents/backend-engineer.md`
- `prompts/backend-task.md`
- 项目经理创建的 `docs/tasks/<Task ID>.md`
- 对应 PRD

职责：

- 输出或维护 API 契约
- 实现后端接口、数据、权限和校验
- 自测后端功能

### 测试窗口

读取：

- `agents/shared-rules.md`
- `agents/qa-engineer.md`
- `prompts/qa-task.md`
- 项目经理创建的 `docs/tasks/<Task ID>.md`
- 对应 PRD、API 契约和实现说明

职责：

- 输出测试计划
- 执行验证
- 输出 QA 报告和验收结论

## 建议

刚开始建议使用单窗口项目经理模式。等项目变复杂、需要并行开发时，再切换到多窗口角色模式。
