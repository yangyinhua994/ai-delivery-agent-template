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
- 当前窗口角色是否匹配任务中的 `Assigned Agent`。

## 发错窗口处理

如果当前窗口角色和任务中的 `Assigned Agent` 不一致，Agent 不得执行任务，必须提示用户切换到正确窗口。

输出格式：

```markdown
## Wrong Window

- Current Window:
- Expected Agent:
- Task File:
- Reason:
- Please Send To:
- Copy Prompt:
```

示例：

```text
当前是前端 Agent 窗口，但任务分配给 Backend Engineer Agent。
请把下面提示语复制到后端窗口：

请读取 docs/tasks/<Task ID>.md，并按后端 Agent 规则完成任务。
完成后请输出 Completion，并说明下一步应该切换到哪个 Agent 窗口。
```

## 阻塞处理

如果无法继续，Agent 不应猜测实现，而是输出：

只有 `docs/process/CONTINUOUS_DELIVERY_RULES.md` 中定义的“必须用户确认的阻塞”才允许暂停等待用户。其它情况应继续推进，并把假设或风险写入文档。

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

## 多窗口下一步提示

在多窗口模式下，Completion 后必须追加：

```markdown
## Next Window

- Go To:
- Can Run In Parallel:
- Files To Pass:
- Copy Prompt:
```

`Copy Prompt` 必须是用户可以直接复制到下一个 Agent 窗口的完整提示语。

项目经理 Agent 是唯一调度中心。非项目经理 Agent 完成后，`Go To` 必须是项目经理窗口。非项目经理 Agent 可以写 `Suggested Next Agent`，但不能直接要求用户跳过项目经理去启动其它 Agent。

如果下一步应该回到项目经理窗口，使用：

```text
请读取以下交付物并继续调度下一步：
- <产出文件>

当前 Agent 已完成 <任务文件>。
请检查交付物是否完整，并由项目经理 Agent 决定下一步调度。
```

只有项目经理 Agent 可以决定下一步并行交给前端和后端。项目经理 Agent 可以分别给出两个提示语：

```text
【发给后端窗口】
请读取 docs/tasks/<Backend Task ID>.md，并按后端 Agent 规则完成任务。
相关输入文件：
- docs/requirements/<Requirement ID>-prd.md
完成后请输出 Completion，并说明下一步应该切换到哪个 Agent 窗口。
```

```text
【发给前端窗口】
请读取 docs/tasks/<Frontend Task ID>.md，并按前端 Agent 规则完成任务。
相关输入文件：
- docs/requirements/<Requirement ID>-prd.md
- docs/api/<Requirement ID>-api-contract.md
完成后请输出 Completion，并说明下一步应该切换到哪个 Agent 窗口。
```
