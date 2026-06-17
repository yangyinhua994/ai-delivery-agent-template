# 技术框架

本模板默认使用以下技术框架。除非用户或项目经理 Agent 明确变更，否则所有 Agent 都必须按此技术栈进行需求拆分、接口设计、开发实现和测试验证。

## 前端

- Framework: Vue
- Recommended Version: Vue 3
- Language: TypeScript, if the project has TypeScript enabled
- Build Tool: Vite, unless the existing project uses another Vue build setup
- UI Layer: Follow the existing project UI library or component style

## 后端

- Framework: Spring Boot
- Persistence: MyBatis-Plus
- Database: MySQL
- Language: Java
- API Style: RESTful JSON API by default

## 默认分层

后端默认分层：

```text
controller
service
service.impl
mapper
entity
dto
vo
config
exception
```

前端默认分层：

```text
src/api
src/views
src/components
src/router
src/stores
src/utils
src/types
```

## Agent 使用规则

- 产品经理 Agent 输出 PRD 时，需要考虑 Vue 前端和 Spring Boot 后端的典型交付边界。
- 后端 Agent 设计接口时，默认使用 Spring Boot Controller + Service + MyBatis-Plus Mapper + MySQL 表结构。
- 后端 Agent 涉及数据库时，必须说明 MySQL 表结构、索引、字段类型和迁移影响。
- 前端 Agent 实现页面时，默认使用 Vue 组件化方式组织页面、状态、接口请求和表单校验。
- 测试 Agent 设计用例时，需要覆盖前端 Vue 页面交互、后端 Spring Boot 接口、MyBatis-Plus 数据读写和 MySQL 数据一致性。

## 变更规则

如果用户希望更换技术栈，项目经理 Agent 必须：

1. 记录变更原因到 `state/decision-log.md`。
2. 更新本文件。
3. 重新评估前端、后端和测试任务。

