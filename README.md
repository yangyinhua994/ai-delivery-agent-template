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

1. 让 AI 读取 [START_PROMPT.md](START_PROMPT.md)。
2. AI 会按提示读取 [START_PROJECT.md](START_PROJECT.md)，检查首次启动状态并加载规则，然后停在“等待用户需求”状态。
3. 你在下一条消息中提供原型地址、需求描述、数据库连接信息、账号、接口文档或其它输入源。
4. 项目经理 Agent 接收需求后，会更新 [state/project-board.md](state/project-board.md)，再按需调度产品、前端、后端、测试 Agent。
5. 每个 Agent 只读取自己被允许读取的输入，只输出自己职责范围内的交付物。

## 当前模式

本模板保留项目经理 Agent 作为调度中枢。

项目经理 Agent 不负责写代码，也不替产品、前端、后端或测试完成具体交付物。它的价值是：

- 接收你的原始需求。
- 判断下一步应该交给哪个 Agent。
- 创建任务文件。
- 检查各 Agent 的交付物。
- 决定是否并行调度前端和后端。
- 在测试后判断需求是否可以交付。

因此，无论是单窗口还是多窗口，项目经理 Agent 都不会被移除。

区别只是：

- 单窗口模式：项目经理 Agent 在同一个窗口内临时切换角色执行。
- 多窗口模式：项目经理 Agent 只负责调度，你手动把任务文件复制到对应角色窗口。

## 单窗口模式

单窗口模式是默认推荐方式，适合个人开发、需求初期、项目规模不大时使用。

使用方式：

```text
请读取 START_PROMPT.md
```

AI 会先读取 [START_PROJECT.md](START_PROJECT.md)，作为项目经理 Agent 完成初始化检查，然后等待你的下一步需求说明。

后续你只需要继续把原型地址、需求描述、数据库连接信息、账号、接口文档或问题清单发给同一个窗口。项目经理 Agent 会在同一个窗口内按需临时切换为产品经理、前端、后端或测试 Agent。

适合场景：

- 一个人推进项目。
- 希望少开窗口，流程简单。
- 先快速从原型或需求跑通完整开发流程。

## 多窗口模式

多窗口模式适合项目较大、希望多个 Agent 分开执行或并行推进时使用。

多窗口模式下，项目经理窗口仍然是唯一需求入口。你只把原始需求交给项目经理窗口，其它角色窗口只接收项目经理创建的任务文件。

每个角色窗口在执行任务前，会先检查任务文件中的 `Assigned Agent` 是否和当前窗口角色一致。如果你复制错窗口，它不会继续执行，而是提示你应该切到哪个窗口，并给出可复制提示语。

项目经理 Agent 是唯一调度中心。产品、前端、后端、测试 Agent 完成后，都必须提示你回到项目经理窗口。只有项目经理 Agent 可以决定下一步去哪个 Agent 窗口，或是否让多个 Agent 并行执行。

每个 Agent 完成后，都会给出可以直接复制到下一步窗口的提示语。非项目经理 Agent 给出的下一步窗口必须是项目经理窗口。

### 1. 项目经理窗口

读取：

```text
prompts/multi-window-project-manager.md
```

或更完整地启动：

```text
请读取 START_PROJECT.md 和 prompts/multi-window-project-manager.md。
你作为项目经理 Agent，只负责接收需求、创建任务、调度其它 Agent、维护状态。
初始化完成后等待我的需求说明。
```

### 2. 产品经理窗口

读取：

```text
prompts/multi-window-product-manager.md
```

产品经理窗口只接收项目经理创建的产品任务文件，例如：

```text
docs/tasks/TASK-<YYYYMMDD>-001-PM.md
```

### 3. 前端窗口

读取：

```text
prompts/multi-window-frontend.md
```

前端窗口只接收项目经理创建的前端任务文件，例如：

```text
docs/tasks/TASK-<YYYYMMDD>-001-FE.md
```

### 4. 后端窗口

读取：

```text
prompts/multi-window-backend.md
```

后端窗口只接收项目经理创建的后端任务文件，例如：

```text
docs/tasks/TASK-<YYYYMMDD>-001-BE.md
```

### 5. 测试窗口

读取：

```text
prompts/multi-window-qa.md
```

测试窗口只接收项目经理创建的测试任务文件，例如：

```text
docs/tasks/TASK-<YYYYMMDD>-001-QA.md
```

### 多窗口协作顺序

```text
你
  -> 项目经理窗口
  -> 创建 docs/tasks/*.md
  -> 分发给产品/前端/后端/测试窗口
  -> 各角色写入自己的交付物
  -> 回到项目经理窗口汇总并继续调度
```

### 多窗口交接示例：前端完成后

下面以前端 Agent 完成任务为例，说明提示语怎么流转。

#### 1. 前端窗口完成后给你的内容

前端 Agent 完成任务后，不会直接让你去测试窗口。它必须让你回到项目经理窗口。

前端窗口应该输出类似内容：

```markdown
## Completion

- Task ID: TASK-<YYYYMMDD>-001-FE
- Requirement ID: REQ-<YYYYMMDD>-001
- Status: done
- Changed Files:
  - src/views/user/UserList.vue
  - src/api/user.ts
- Verification:
  - 已完成页面自测
  - 已按 API 契约完成联调适配
- Risks:
  - 真实后端环境未启动时，部分接口仅按契约验证
- Next Suggested Agent:
  - 建议回到项目经理窗口，由项目经理决定是否调度测试 Agent

## Next Window

- Go To: 项目经理窗口
- Can Run In Parallel: 否，由项目经理判断
- Files To Pass:
  - docs/tasks/TASK-<YYYYMMDD>-001-FE.md
  - docs/requirements/REQ-<YYYYMMDD>-001-prd.md
  - docs/api/REQ-<YYYYMMDD>-001-api-contract.md
- Copy Prompt:

请读取前端 Agent 的交付物并继续调度下一步：
- docs/tasks/TASK-<YYYYMMDD>-001-FE.md
- docs/requirements/REQ-<YYYYMMDD>-001-prd.md
- docs/api/REQ-<YYYYMMDD>-001-api-contract.md

前端 Agent 已完成任务。请检查前端实现说明和自测结果，并由项目经理 Agent 决定下一步调度。
```

#### 2. 你复制给项目经理窗口

你只需要把 `Copy Prompt` 复制到项目经理窗口：

```text
请读取前端 Agent 的交付物并继续调度下一步：
- docs/tasks/TASK-<YYYYMMDD>-001-FE.md
- docs/requirements/REQ-<YYYYMMDD>-001-prd.md
- docs/api/REQ-<YYYYMMDD>-001-api-contract.md

前端 Agent 已完成任务。请检查前端实现说明和自测结果，并由项目经理 Agent 决定下一步调度。
```

#### 3. 项目经理窗口收到后应该做什么

项目经理 Agent 收到后会：

1. 读取前端任务文件和相关交付物。
2. 判断前端是否真的完成。
3. 检查是否还需要后端、产品或测试介入。
4. 更新 `state/project-board.md`。
5. 创建下一步任务，或调度已有任务。
6. 给出下一步窗口和可复制提示语。

如果项目经理判断可以进入测试，它会输出类似内容：

```markdown
## 调度结果

- Requirement ID: REQ-<YYYYMMDD>-001
- 当前状态: ready_for_qa
- 已检查交付物:
  - docs/tasks/TASK-<YYYYMMDD>-001-FE.md
  - docs/requirements/REQ-<YYYYMMDD>-001-prd.md
  - docs/api/REQ-<YYYYMMDD>-001-api-contract.md
- 下一步窗口: 测试窗口
- 任务文件: docs/tasks/TASK-<YYYYMMDD>-001-QA.md

## Copy Prompt

【发给测试窗口】
请读取 docs/tasks/TASK-<YYYYMMDD>-001-QA.md，并按测试 Agent 规则完成任务。
相关输入文件：
- docs/requirements/REQ-<YYYYMMDD>-001-prd.md
- docs/api/REQ-<YYYYMMDD>-001-api-contract.md
- docs/tasks/TASK-<YYYYMMDD>-001-FE.md

完成后请输出 Completion，并说明下一步应该切换到哪个 Agent 窗口。
```

#### 4. 你再复制给测试窗口

你把项目经理给出的 `Copy Prompt` 复制到测试窗口即可。

测试 Agent 完成后，也会让你回到项目经理窗口，由项目经理判断：

- 是否验收完成。
- 是否有缺陷要回前端或后端修复。
- 是否需要重新测试。

#### 5. 其它 Agent 完成时也是同样规则

- 产品经理完成后：回项目经理窗口，由项目经理决定是否调度前端、后端或测试。
- 后端完成后：回项目经理窗口，由项目经理决定是否调度前端联调或测试。
- 前端完成后：回项目经理窗口，由项目经理决定是否调度测试或修复。
- 测试完成后：回项目经理窗口，由项目经理决定验收、修复或重新测试。

非项目经理 Agent 可以写“建议下一步”，但不能直接调度其它 Agent。真正的下一步执行提示语由项目经理 Agent 给出。

选择建议：

- 不确定用哪种时，先用单窗口模式。
- 需要并行开发、减少上下文干扰时，再切换多窗口模式。

## 从单窗口切换到多窗口

如果项目一开始使用单窗口模式，后面项目变大，需要切换为多窗口模式，可以让当前单窗口里的项目经理 Agent 做切换准备。

在当前单窗口中发送：

```text
请读取 prompts/switch-single-to-multi-window.md，并作为项目经理 Agent 准备从单窗口模式切换到多窗口模式。
```

项目经理 Agent 会：

1. 汇总当前项目状态。
2. 更新 `state/project-board.md`。
3. 检查已有 PRD、API 契约、任务文件、测试计划和 QA 报告。
4. 创建或修正 `docs/tasks/` 下的多窗口任务文件。
5. 标记哪些任务已完成，哪些任务需要交给多窗口 Agent。
6. 输出每个 Agent 窗口的启动提示语。

切换后，你需要打开对应窗口：

- 项目经理窗口：读取 `prompts/multi-window-project-manager.md`
- 产品经理窗口：读取 `prompts/multi-window-product-manager.md`
- 后端窗口：读取 `prompts/multi-window-backend.md`
- 前端窗口：读取 `prompts/multi-window-frontend.md`
- 测试窗口：读取 `prompts/multi-window-qa.md`

切换后的规则不变：

- 项目经理 Agent 是唯一调度中心。
- 非项目经理 Agent 只执行项目经理创建的任务文件。
- 非项目经理 Agent 完成后必须回到项目经理窗口。
- 是否并行执行，由项目经理 Agent 决定。

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
  -> 项目经理：检查 PRD，拆分前端/后端/测试任务
  -> 后端：接口、数据、服务逻辑
  -> 项目经理：检查后端交付物，决定下一步
  -> 前端：页面、交互、联调
  -> 项目经理：检查前端交付物，决定下一步
  -> 测试：测试用例、执行验证、缺陷报告
  -> 项目经理：汇总状态、确认是否交付
```

如果项目经理判断前后端可以并行，会同时创建后端和前端任务。即使并行执行，各 Agent 完成后也必须回到项目经理 Agent，由项目经理继续调度。

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
- [START_PROMPT.md](START_PROMPT.md)：最简启动入口，懒人专用
- [START_PROJECT.md](START_PROJECT.md)：推荐使用的单文件启动入口，首次启动后等待你继续提供需求
- [FIRST_RUN_CHECKLIST.md](FIRST_RUN_CHECKLIST.md)：首次启动模板检查清单
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
- [prompts/switch-single-to-multi-window.md](prompts/switch-single-to-multi-window.md)：单窗口切换到多窗口提示语
- [workflows/00-overview.md](workflows/00-overview.md)：整体流程
- [workflows/03-handoff-protocol.md](workflows/03-handoff-protocol.md)：交接协议
- [workflows/04-routing-matrix.md](workflows/04-routing-matrix.md)：项目经理调度矩阵
