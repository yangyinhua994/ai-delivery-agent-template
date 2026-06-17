# AI 自动化协作模板

这是一个面向产品研发流程的多 Agent 模板。核心原则是：

- 项目经理 Agent 只接收需求、拆分任务、调度角色、维护状态。
- 产品经理 Agent 只把原型、问题描述、业务目标解析成可执行需求。
- 前端 Agent 只根据需求和接口契约实现前端。
- 后端 Agent 只根据需求和接口契约实现后端。
- 测试 Agent 只验证需求是否被正确实现，并输出缺陷报告。

你可以把这个仓库作为一个工作区模板使用。后续你只需要把原型地址、需求描述或问题清单交给「项目经理 Agent」，它会决定下一步该交给哪个 Agent。

## 推荐目录

```text
.
├── agents/                 # 各角色 Agent 的职责、输入、输出和禁止事项
├── docs/
│   ├── api/                # 接口契约
│   ├── architecture/       # 技术框架和架构约束
│   ├── requirements/       # PRD、用户故事、验收标准
│   ├── reports/            # 测试报告、缺陷报告、验收结论
│   └── tasks/              # 拆分后的执行任务
├── inbox/                  # 你提交给项目经理的原始需求
├── state/                  # 项目经理维护的项目看板和决策记录
└── workflows/              # 标准协作流程
```

## 最小使用方式

1. 让 AI 先读取 [START_HERE.md](START_HERE.md)。
2. 默认使用“单窗口项目经理模式”，由项目经理 Agent 接收你的所有需求。
3. 把你的需求写入 [inbox/request-template.md](inbox/request-template.md)，或直接在对话中给项目经理 Agent。
4. 项目经理 Agent 会先更新 [state/project-board.md](state/project-board.md)，再按需调度产品、前端、后端、测试 Agent。
5. 每个 Agent 只读取自己被允许读取的输入，只输出自己职责范围内的交付物。

## 默认技术框架

- 前端：Vue，默认 Vue 3。
- 后端：Spring Boot。
- 持久层：MyBatis-Plus。
- 数据库：MySQL。

详细约束见 [docs/architecture/TECH_STACK.md](docs/architecture/TECH_STACK.md)。

## 持续交付规则

项目经理 Agent 的最终目标是全部页面、前端、后端、测试和验收完成。

单个 Agent 的最终目标不是完成全部页面，而是完成自己职责内的交付物并写入文档，等待项目经理 Agent 下一步调度。

除非出现必须用户确认的阻塞，否则不要停在计划、分析或部分完成阶段。

详细规则见 [docs/process/CONTINUOUS_DELIVERY_RULES.md](docs/process/CONTINUOUS_DELIVERY_RULES.md)。

## 标准交付顺序

```text
用户需求
  -> 项目经理：澄清、编号、确定调度
  -> 产品经理：原型解析、PRD、验收标准
  -> 项目经理：拆分前端/后端/测试任务
  -> 后端：接口、数据、服务逻辑
  -> 前端：页面、交互、联调
  -> 测试：测试用例、执行验证、缺陷报告
  -> 项目经理：汇总状态、确认是否交付
```

## Agent 之间的硬性边界

- 产品经理不写代码。
- 前端不改后端逻辑，除非任务明确授权。
- 后端不改前端 UI，除非任务明确授权。
- 测试不直接修复问题，只报告问题和复现路径。
- 项目经理不替其它 Agent 实现，只负责调度、验收状态和风险管理。

## 常见输入示例

```text
原型地址：https://example.com/prototype
目标：把原型转成一个可上线的后台管理系统。
补充：优先实现登录、用户列表、用户详情、角色权限。
```

```text
修改问题：
1. 登录页按钮在移动端超出屏幕。
2. 用户列表搜索后分页没有重置。
3. 新建角色接口缺少权限字段校验。
```

## 关键文件

- [START_HERE.md](START_HERE.md)：后续让 AI 首先读取的启动入口
- [agent-manifest.yaml](agent-manifest.yaml)：机器可读的 Agent 配置、权限和调度规则
- [docs/architecture/TECH_STACK.md](docs/architecture/TECH_STACK.md)：默认技术框架
- [docs/process/CONTINUOUS_DELIVERY_RULES.md](docs/process/CONTINUOUS_DELIVERY_RULES.md)：持续交付规则
- [agents/project-manager.md](agents/project-manager.md)：项目经理 Agent 主提示词
- [agents/product-manager.md](agents/product-manager.md)：产品经理 Agent 主提示词
- [agents/frontend-engineer.md](agents/frontend-engineer.md)：前端 Agent 主提示词
- [agents/backend-engineer.md](agents/backend-engineer.md)：后端 Agent 主提示词
- [agents/qa-engineer.md](agents/qa-engineer.md)：测试 Agent 主提示词
- [prompts/project-manager-start.md](prompts/project-manager-start.md)：可直接复制使用的项目经理启动提示词
- [prompts/single-window-start.md](prompts/single-window-start.md)：单窗口模式完整启动提示语
- [prompts/multi-window-start.md](prompts/multi-window-start.md)：多窗口模式完整启动提示语
- [workflows/00-overview.md](workflows/00-overview.md)：整体流程
- [workflows/03-handoff-protocol.md](workflows/03-handoff-protocol.md)：交接协议
- [workflows/04-routing-matrix.md](workflows/04-routing-matrix.md)：项目经理调度矩阵
