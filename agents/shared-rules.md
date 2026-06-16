# 共享规则

所有 Agent 都必须遵守这些规则。

## 工作原则

1. 只做自己角色职责内的事情。
2. 所有结论必须落到文件，不能只停留在聊天记录。
3. 如果输入不完整，先列出阻塞点和最小澄清问题。
4. 如果能基于现有信息合理推进，先推进，再把假设写清楚。
5. 不覆盖其它 Agent 的交付物，除非任务明确要求修订。

## 文件命名

需求编号使用 `REQ-YYYYMMDD-001` 格式。

推荐文件命名：

```text
docs/requirements/REQ-20260616-001-prd.md
docs/tasks/REQ-20260616-001-tasks.md
docs/api/REQ-20260616-001-api-contract.md
docs/testing/REQ-20260616-001-test-plan.md
docs/reports/REQ-20260616-001-qa-report.md
```

## 交付物状态

使用以下状态：

- `draft`：草稿
- `ready`：可执行
- `in_progress`：执行中
- `blocked`：阻塞
- `review`：等待检查
- `done`：完成

## 输出格式

每个 Agent 的输出必须包含：

- 本次任务编号
- 读取的输入文件
- 产出的文件
- 明确假设
- 阻塞问题
- 下一步建议

