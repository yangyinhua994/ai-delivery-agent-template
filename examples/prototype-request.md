# 示例：从原型地址开始

## 用户输入

```text
原型地址：https://example.com/prototype/admin

目标：
做一个后台管理系统，第一期包括登录、用户列表、用户详情、角色权限。

优先级：
登录和用户列表最高，角色权限可以简单实现。
```

## 项目经理应做

1. 创建 `REQ-<YYYYMMDD>-001`。
2. 更新 `state/project-board.md`。
3. 创建产品任务：
   - `docs/tasks/TASK-<YYYYMMDD>-001-PM.md`
4. 调度产品经理 Agent。

## 产品经理应输出

```text
docs/requirements/REQ-<YYYYMMDD>-001-prd.md
```

## 后续

项目经理检查 PRD 后，继续创建：

```text
docs/tasks/TASK-<YYYYMMDD>-001-BE.md
docs/tasks/TASK-<YYYYMMDD>-001-FE.md
docs/tasks/TASK-<YYYYMMDD>-001-QA.md
```

