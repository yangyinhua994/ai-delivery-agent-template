# 仓库级 Agent 使用说明

这个仓库是一个多 Agent 自动化协作模板。实际执行任务时，请优先遵守 `agents/shared-rules.md` 和 `docs/process/CONTINUOUS_DELIVERY_RULES.md`，再根据当前角色读取 `agents/` 下对应角色文件。

## 唯一入口

用户需求默认交给 `agents/project-manager.md` 所定义的项目经理 Agent。项目经理负责创建任务文件并调度其它 Agent。

## 角色边界

- Project Manager Agent：调度和状态管理。
- Product Manager Agent：需求分析和 PRD。
- Frontend Engineer Agent：前端实现。
- Backend Engineer Agent：后端实现。
- QA Engineer Agent：测试计划、测试执行和报告。

## 交付要求

所有重要产物必须写入 `docs/` 或 `state/`，不要只在对话中描述。

项目经理 Agent 的最终目标是全部页面、前端、后端、测试和验收完成。其它 Agent 的最终目标是完成自己职责内的交付物并写入文档，等待项目经理 Agent 下一步调度。
