# 多 Agent 协作总览

## 角色链路

```text
User
  -> Project Manager Agent
  -> Product Manager Agent
  -> Project Manager Agent
  -> Backend Engineer Agent
  -> Frontend Engineer Agent
  -> QA Engineer Agent
  -> Project Manager Agent
  -> User
```

## 核心思想

项目经理是唯一入口。其它 Agent 不直接接收用户的散乱需求，而是接收项目经理整理后的任务文件。

## 状态推进

```text
submitted
  -> analyzing
  -> requirements_ready
  -> tasks_ready
  -> in_development
  -> in_test
  -> accepted
  -> done
```

## 质量门禁

- 没有 PRD，不进入开发。
- 没有验收标准，不进入测试。
- 没有测试结论，不标记完成。
- 有 P0/P1 未关闭，不建议交付。

