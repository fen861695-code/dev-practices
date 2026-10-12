# dev-practices

团队开发全流程规范（前端 · 后端），以 Skill 形式发布，供研发团队与 AI 编码助手共同遵循。

## 内容

- **SKILL.md**：Skill 主入口（描述、使用方式、红线、文件索引）。
- **rules/**：按研发环节拆分的可执行规则（流程、架构、Git、结构、环境、前端、后端、数据库、评审、测试、CI/CD、文档、安全、AI 辅助、可观测性、协作）。
- **checklists/**：可直接逐项核对的检查清单（新项目、本地自检、PR 评审、DoD、发布）。

## 使用方式

- 作为 Skill 安装：将本目录放入 agent 的 skill 根目录，或直接引用 `SKILL.md`。
- 作为团队规范：按 `rules/` 与 `checklists/` 组织团队文档，随版本迭代维护。

## 规范来源

综合参考以下公开实践整理（详见正文附录）：

- Google Engineering Practices（代码评审）
- elsewhencode/project-guidelines（项目全流程最佳实践）
- Microsoft Code-with Engineering Playbook（工程基础与检查单）
- CISA Development Guide（工程工具链与安全）
- Microsoft REST API Guidelines（API 设计）
- Conventional Commits（提交信息规范）
- OWASP Top 10（Web 安全基线）
- Google Core Web Vitals（前端性能指标）

## 许可

本仓库内容以 MIT 许可发布（见 LICENSE）。
