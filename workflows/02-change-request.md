# 修改问题处理流程

## 适用场景

用户给出问题清单、缺陷反馈、体验优化或局部需求变更。

## 分类规则

- 页面展示、布局、交互：优先前端 Agent。
- 接口返回、数据错误、权限、校验：优先后端 Agent。
- 需求表达不清或影响范围不明：先产品经理 Agent。
- 已修复待验证：测试 Agent。

## 流程

1. 项目经理把每个问题拆成独立条目。
2. 项目经理判断归属 Agent。
3. 如果问题存在产品歧义，先交给产品经理补充验收标准。
4. 前端或后端 Agent 修复。
5. 测试 Agent 回归验证。
6. 项目经理关闭问题或重新打开。

## 缺陷任务示例

```markdown
# Agent Task

- Task ID: TASK-20260616-002-FE
- Requirement ID: REQ-20260616-002
- Assigned Agent: Frontend Engineer Agent
- Priority: P2
- Status: ready
- Source: inbox/request-template.md
- Inputs:
  - docs/reports/REQ-20260616-002-qa-report.md
- Expected Outputs:
  - 前端修复
  - 自测说明
- Acceptance Criteria:
  - 登录页按钮在 375px 宽度下不超出屏幕
  - 主流程登录仍可正常执行
```

