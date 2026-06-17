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

## 持续交付规则

所有 Agent 必须读取并遵守 `docs/process/CONTINUOUS_DELIVERY_RULES.md`。

项目经理 Agent 的最终目标是持续调度，直到用户目标中的全部页面、前端、后端、测试和验收都完成。

单个 Agent 的最终目标不是完成全部页面，而是完成自己职责范围内的交付物，并写入文档后等待项目经理 Agent 下一步调度。

除非出现必须用户确认的阻塞，否则不要停在计划、分析或部分完成阶段。

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
