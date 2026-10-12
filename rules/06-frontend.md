# 前端开发规则（06-frontend）

## 语言与工程

- 默认 TypeScript；禁止用 any 绕过类型检查。
- 统一 ESLint + Prettier，风格由工具强制；统一包管理器并提交 lockfile。
- Node 与框架版本在 .nvmrc / engines 声明。

## HTML / CSS

- 使用语义化标签；页面包含 lang、title、meta description；图片必须有 alt。
- 表单控件关联 label；交互优先原生 button / a。
- CSS 命名用 BEM，嵌套不超过三层，避免 ID 选择器。
- 设计令牌（颜色、间距、字号）统一收口到变量或设计系统，禁止魔法值。
- 响应式断点统一（576 / 768 / 992 / 1200），优先移动优先。
- 动画尽量使用 transform / opacity，避免重排重绘。

## JS / TS

- 变量优先 const，禁止 var；命名语义化，禁止拼音与无意义缩写。
- 函数单一职责；遍历优先 map / filter / reduce。
- 异步优先 async / await；Promise 必须处理异常。
- 错误统一处理路径，前端展示与上报分离，禁止把原始堆栈展示给用户。
- 为接口响应、状态、props 定义显式类型。

## 组件 / 状态 / 请求

- 组件高内聚低耦合；props 扁平化并显式声明类型；单向数据流。
- 组件内部状态最小化；跨组件共享状态收敛到状态管理。
- 请求统一走封装层，统一鉴权头、超时、错误码与取消；处理竞态。
- 敏感数据不得写入 localStorage 等持久存储（除非评估后必须并加密）。

## 性能 / 可访问性 / 安全 / 测试

- 首屏：路由级代码分割、关键资源预加载，LCP 目标建议 2.5s 内；持续观测 LCP / INP / CLS。
- 对比度满足 WCAG AA；全部交互可键盘完成；合理使用 ARIA；考虑 prefers-reduced-motion。
- 渲染用户内容使用框架默认转义，禁止直接拼接 HTML（v-html / dangerouslySetInnerHTML 需逐处评审）。
- 登录态使用 HttpOnly Cookie 或受保护存储；依赖定期扫描。
- 纯函数与工具逻辑必须有单测；关键用户路径有 E2E；测试断言关注行为而非实现。
