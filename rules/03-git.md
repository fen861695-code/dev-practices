# Git 与分支规则（03-git）

## 分支模型

- main（master）：生产分支，受保护，禁止直接推送。
- develop：集成分支，受保护。
- feature/&lt;描述&gt;：功能分支，从 develop 切出，PR 合并回 develop。
- fix/&lt;描述&gt;：缺陷修复分支。
- release/&lt;版本号&gt;：发版分支，仅允许修复类提交。
- hotfix/&lt;描述&gt;：线上紧急修复，从 main 切出，修复后同时合回 main 与 develop。

## 规则

1. 所有开发在特性分支进行，禁止直接在 main / develop 提交。
2. 推送 PR 前同步远端 develop 并交互式 rebase，解决冲突。
3. PR 合并前必须通过 CI 检查与至少一次评审。
4. 合并后删除已合并的特性分支。
5. main / develop 开启分支保护：禁止强制推送、要求 PR 与检查通过。
6. 提交不包含敏感信息；大文件与构建产物不得入库。

## Commit message（Conventional Commits）

```
<type>[(<scope>)]: <subject>

[body]
```

- type：feat、fix、docs、style、refactor、perf、test、build、ci、chore、revert
- subject：祈使句、不超过 50 字符、不以句号结尾
- body：说明"为什么"，可关联 issue

## 合并与发布

- PR 采用 Squash / Rebase Merge，保持主干线性历史。
- 发版从 develop 切 release 分支，成功后 main 打 tag（如 v1.4.0）。
- CHANGELOG 与提交信息对应。
