# 项目结构与命名规则（04-structure-naming）

## 通用原则

- 目录按"职责"组织，让新成员快速定位代码。
- 业务代码与通用能力分离；公共代码可抽取为独立包或模块。
- 每个目录都能回答"这是干什么的"，无说明的目录不保留。

## 前端目录（推荐）

```
src/
├── api/ components/ pages/ hooks/ router/
├── stores/ styles/ types/ utils/ tests/
└── main.ts
```

## 后端目录（推荐）

```
src/
├── controller/ service/ repository/ domain/
├── middleware/ dto/ config/ jobs/ utils/
└── main.ts
```

## 命名约定

| 对象 | 约定 | 示例 |
| --- | --- | --- |
| 前端组件 / 文件 | 组件 PascalCase；普通文件 camelCase | UserCard.tsx、userService.ts |
| 变量 / 函数 | camelCase；常量 UPPER_SNAKE_CASE | userList、MAX_RETRY |
| CSS 类名 | BEM：block__element--modifier | card__title--active |
| 后端类 / 接口 | PascalCase | UserService |
| 后端方法 | camelCase，动词开头 | createUser、findById |
| 数据库表 | snake_case 复数 | user_accounts |
| 数据库字段 | snake_case，主键 id，外键 xxx_id | created_at、user_id |
| 环境变量 | UPPER_SNAKE_CASE，应用前缀 | APP_ENV、DB_HOST |
