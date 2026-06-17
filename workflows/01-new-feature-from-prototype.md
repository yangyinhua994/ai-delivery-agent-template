# 从原型创建新功能

## 适用场景

用户给出原型地址、设计稿、截图或一个新功能想法。

## 流程

1. 用户把原型地址或描述放入 `inbox/request-template.md`。
2. 项目经理创建 Requirement ID。
3. 项目经理调度产品经理 Agent。
4. 产品经理输出 `docs/requirements/<Requirement ID>-prd.md`。
5. 项目经理检查 PRD 是否包含验收标准。
6. 项目经理拆分前端、后端、测试任务。
7. 后端优先输出或确认 API 契约。
8. 前端根据 PRD 和 API 契约实现页面与交互。
9. 测试根据 PRD 和 API 契约输出测试计划并执行。
10. 项目经理汇总 QA 结论，决定交付或返工。

## 项目经理调度示例

```markdown
# Agent Task

- Task ID: TASK-<YYYYMMDD>-001-PM
- Requirement ID: REQ-<YYYYMMDD>-001
- Assigned Agent: Product Manager Agent
- Priority: P1
- Status: ready
- Source: inbox/request-template.md
- Inputs:
  - Prototype URL: https://example.com/prototype
- Expected Outputs:
  - docs/requirements/REQ-<YYYYMMDD>-001-prd.md
- Acceptance Criteria:
  - 页面范围完整
  - 每个核心功能都有验收标准
  - 未决问题明确列出
```

