# 环境与本地开发规则（05-environment）

## 开发环境标准

- 语言与运行时版本统一管理（.nvmrc、.python-version 等），禁止版本漂移。
- 编辑器统一配置：EditorConfig、格式化插件，风格由配置强制。
- 优先容器化开发：Dockerfile / devcontainer / docker-compose 一条命令拉起全部本地依赖。
- 本地与生产行为差异（OS、时区、依赖版本）显式记录。

## 依赖与配置

- 依赖锁定版本并提交锁文件；克隆后一条命令可还原安装。
- 配置文件不入库，提供 .env.example 模板并注释每项用途。
- 本地使用与生产不同的凭据与数据。
- 构建脚本统一命名（install / dev / test / build / lint）并写入 README。

## 本地自检

提交前核对：lint 通过 → 类型检查通过 → 单元测试通过 → 构建成功 → 本地冒烟可运行。
