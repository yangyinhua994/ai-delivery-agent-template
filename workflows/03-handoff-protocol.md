# Agent 交接协议

## 交接对象

Agent 之间不直接口头交接，必须通过文件交接。

## 交接包

每次交接至少包含：

- 任务文件：`docs/tasks/<Task ID>.md`
- 需求文件：`docs/requirements/<Requirement ID>-prd.md`
- 接口契约：`docs/api/<Requirement ID>-api-contract.md`，如适用
- 测试计划或 QA 报告：如适用

## 交接检查

接收任务的 Agent 必须先检查：

- Requirement ID 是否一致。
- 输入文件是否存在。
- 任务范围是否清楚。
- 验收标准是否可验证。
- 是否有阻塞问题。

## 阻塞处理

如果无法继续，Agent 不应猜测实现，而是输出：

```markdown
## Blocked

- Blocking Reason:
- Missing Information:
- Suggested Owner:
- Minimal Question:
```

## 完成回传

任务完成后，Agent 必须输出：

```markdown
## Completion

- Task ID:
- Requirement ID:
- Status:
- Changed Files:
- Verification:
- Risks:
- Next Suggested Agent:
```

