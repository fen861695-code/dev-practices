---
name: dev-practices
description: 团队开发全流程规范（前端 · 后端）。当需要按团队规范进行代码编写与评审、提交 PR、编写 commit message、设计 API、数据库迁移、编写测试、配置 CI/CD、处理安全与依赖扫描、配置可观测性、使用 AI 辅助开发，或需要套用新项目初始化、本地自检、评审、完成定义（DoD）、发布等检查清单时使用。覆盖研发流程、架构选型、Git 与分支、目录命名、前端与后端开发、代码评审、测试、CI/CD、文档、安全、可观测性、AI 辅助开发等全部研发环节。
---

# 开发全流程规范（dev-practices）

团队研发全流程的统一规范，供开发、评审、测试、运维与 AI 编码助手在各类研发任务中遵循。

## 何时使用

- 编写或修改代码、组件、接口时，先读取对应环节的规则文件，再动手。
- 提交 PR / 评审代码 / 设计 API / 改数据库 / 配置流水线 / 处理安全问题时，读取对应规则与检查清单。
- 新项目启动、任务验收、发布前，按对应检查清单逐项核对。

## 如何使用

1. 按任务类型读取 `rules/` 下对应的规则文件（1 个或相邻多个），以其中 MUST / SHOULD 条款为执行标准。
2. 涉及"提交前 / 评审 / 发布 / 新项目 / 完成"等动作时，读取 `checklists/` 下对应清单并逐项核对。
3. 规则冲突时：安全相关条款优先；任务明确要求优先于通用建议；不一致时按最严格的执行并说明理由。

## 核心红线（任何时候不得违反）

- 禁止直接把敏感信息（密钥、令牌、个人数据、生产数据）写入代码、日志或提交记录。
- 所有进入主干的代码必须经过评审与 CI 检查，禁止绕过。
- 数据库变更必须走迁移脚本与评审，禁止手工改库。
- AI 生成的代码与手写代码同等标准，必须人工审查并通过全部检查。
- 外部输入必须校验，默认拒绝未授权的访问。

## 文件索引

| 场景 | 规则文件 | 检查清单 |
| --- | --- | --- |
| 需求到上线流程 | `rules/01-process.md` | - |
| 技术选型 / 架构评审 | `rules/02-architecture.md` | - |
| 分支 / 提交 / 合并 | `rules/03-git.md` | - |
| 目录与命名 | `rules/04-structure-naming.md` | - |
| 本地开发环境 | `rules/05-environment.md` | `checklists/local-check.md` |
| 前端开发 | `rules/06-frontend.md` | - |
| 后端 / API | `rules/07-backend.md` | - |
| 数据库设计 / 迁移 | `rules/08-database.md` | - |
| 代码评审 | `rules/09-review.md` | `checklists/pr-review.md` |
| 测试 | `rules/10-testing.md` | - |
| CI/CD 与交付 | `rules/11-cicd.md` | `checklists/release.md` |
| 文档 | `rules/12-docs.md` | - |
| 安全 | `rules/13-security.md` | - |
| AI 辅助开发 | `rules/14-ai-assist.md` | - |
| 可观测性 / 运维 | `rules/15-observability.md` | - |
| 协作 / DoR / DoD | `rules/16-collaboration.md` | `checklists/dod.md`、`checklists/new-project.md` |
