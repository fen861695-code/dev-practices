# dev-practices

团队开发全流程规范（前端 · 后端），以 Skill 形式发布，供研发团队与 AI 编码助手共同遵循。仓库包含**两个版本**：面向有经验者的正式版，以及面向零基础初学者的导师版。

## 仓库内容

### 1. 正式版（仓库根目录）

- **SKILL.md**：Skill 主入口（描述、使用方式、红线、文件索引）。
- **rules/**：按研发环节拆分的可执行规则（流程、架构、Git、结构、环境、前端、后端、数据库、评审、测试、CI/CD、文档、安全、AI 辅助、可观测性、协作，共 16 个）。
- **checklists/**：可直接逐项核对的检查清单（新项目、本地自检、PR 评审、DoD、发布，共 5 个）。

### 2. 零基础版（beginner/）

面向零编程经验初学者的"开发导师"：一次一步、大白话讲解、代码逐行解释、边做边学，并引导学习者边开发边记录、最终产出项目开发经验文档。详见 [`beginner/README.md`](beginner/README.md)。

```
beginner/
├── SKILL.md                    # 导师模式主入口
├── guide/                      # 12 步分步引导
├── checkpoints/                # 每步完成确认
├── glossary.md                 # 术语大白话词典
└── project-journal-template.md # 项目开发日志模板
```

## 我该用哪个版本

| 你的情况 | 推荐版本 |
| --- | --- |
| 有开发经验，需要团队规范与速查清单 | 正式版（根目录） |
| 零基础，想被一步一步带着做项目、边做边学 | 零基础版（beginner/） |

## 使用方式

- 作为 Skill 安装：将对应目录放入 agent 的 skill 根目录，或直接引用其 `SKILL.md`。
- 作为团队规范：按 `rules/` 与 `checklists/` 组织团队文档，随版本迭代维护。
- 零基础学习：加载 `beginner/SKILL.md`，告诉 AI 你想做什么，然后跟着每一步动手。

## 规范来源

综合参考公开工程实践整理，作为致谢与出处：

- Google Engineering Practices（代码评审）
- elsewhencode/project-guidelines（项目全流程最佳实践）
- Microsoft Code-with Engineering Playbook（工程基础与检查单）
- CISA Development Guide（工程工具链与安全）
- Microsoft REST API Guidelines（API 设计）
- Conventional Commits（提交信息规范）
- OWASP Top 10（Web 安全基线）
- Google Core Web Vitals（前端性能指标）

## 文档语言

- 中文：README.md、beginner/README.md
- English：[README.en.md](README.en.md)、[beginner/README.en.md](beginner/README.en.md)

## 许可

本仓库内容以 MIT 许可发布（见 [LICENSE](LICENSE)）。
