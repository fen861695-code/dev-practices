# 第 7 步：前后端连起来

> 本步目标：让前端通过 fetch 调用后端四个接口，实现"加载真数据、添加、勾选完成、删除"的完整闭环，串通整条数据流动。

## 1. 进度（导师话术）

"这一步把'大堂'和'厨房'接通：页面上的每个操作都会真正调用后端、更新数据库，一个能用的待办清单就此诞生。"

## 2. 为什么

- 前后端各自做好后，联调才能让产品真正完整可用。
- 这是把第 2 步设计的"数据流动"真正实现的一步，理解了它，就理解了绝大多数 Web 应用的工作方式。

## 3. 概念扫盲

- **fetch**：浏览器内置的"点单电话"，用它向接口发请求、拿响应。
- **异步（async / await）**：向后端点单后，菜要时间做，程序会"在旁边等响应而不卡住页面"，响应回来后再继续处理。`await` 就是"等这一步拿到结果再往下走"。
- **同源**：当前端页面和后端接口来自同一个地址（这里都是 localhost:3000）时叫同源，沟通最省事，不会有跨域限制。我们把前端放在 public 由 Express 一起提供，正是为了同源。

## 4. 跟着做

把 `public/app.js` 整体替换为下面内容（去掉假数据，全部改走后端）：

```javascript
const todoList = document.getElementById('todo-list');
const todoInput = document.getElementById('todo-input');
const addBtn = document.getElementById('add-btn');

// 从后端获取全部待办并渲染
async function loadTodos() {
  const res = await fetch('/api/todos');        // 发 GET 请求
  const todos = await res.json();               // 把响应转成数据
  render(todos);
}

// 根据数据画出列表
function render(todos) {
  todoList.innerHTML = '';
  todos.forEach(function (todo) {
    const li = document.createElement('li');
    li.className = 'todo-item' + (todo.done ? ' done' : '');

    const checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.checked = todo.done;
    checkbox.addEventListener('change', function () {
      toggleTodo(todo.id);                       // 勾选时调用"改"接口
    });

    const span = document.createElement('span');
    span.className = 'text';
    span.textContent = todo.text;

    const delBtn = document.createElement('button');
    delBtn.className = 'delete-btn';
    delBtn.textContent = '删除';
    delBtn.addEventListener('click', function () {
      deleteTodo(todo.id);                       // 点删除时调用"删"接口
    });

    li.appendChild(checkbox);
    li.appendChild(span);
    li.appendChild(delBtn);
    todoList.appendChild(li);
  });
}

// 添加待办
async function addTodo() {
  const text = todoInput.value.trim();
  if (!text) return;                             // 空内容不发送
  await fetch('/api/todos', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ text: text })         // 把数据转成 JSON 发送
  });
  todoInput.value = '';                          // 清空输入框
  loadTodos();                                   // 重新加载列表
}

// 切换完成状态
async function toggleTodo(id) {
  await fetch('/api/todos/' + id, { method: 'PATCH' });
  loadTodos();
}

// 删除待办
async function deleteTodo(id) {
  await fetch('/api/todos/' + id, { method: 'DELETE' });
  loadTodos();
}

addBtn.addEventListener('click', addTodo);
todoInput.addEventListener('keydown', function (e) {
  if (e.key === 'Enter') addTodo();              // 按回车也能添加
});

loadTodos();   // 打开页面先加载真数据
```

逐块讲解：
- 每个操作都是同一个套路：`fetch` 发请求（GET 可省略 method；其他操作指定 method，POST 还要在 body 里带 JSON 数据并声明 Content-Type）→ `await` 等响应 → 重新 `loadTodos()` 让页面和数据库保持一致。
- 添加后清空输入框、支持回车提交，是常见的体验细节。
- 勾选框的 `change` 事件、按钮的 `click` 事件，把"用户操作"和"调用接口"绑定起来。

## 5. 检查一下

让小白在网页上完整走一遍并截图/录屏：
1. 添加两条待办 → 列表立即出现。
2. 勾选其中一条 → 出现删除线。
3. 刷新页面（F5）→ 数据还在（来自数据库）。
4. 删除一条 → 列表立即更新。
全部符合 = 全栈闭环打通，这是本项目最有成就感的一步。

## 6. 学到了什么

1. fetch + async/await 是前端调用接口的标准方式：发请求、等响应、更新页面。
2. 每次操作后重新加载数据，保证页面显示与数据库一致。
3. 一个完整 Web 应用 = 前端发请求 → 后端处理并读写数据库 → 返回结果 → 前端更新，这条链路你已经亲手走通。

## 7. 记到项目文档

在 `PROJECT_JOURNAL.md` 记录：fetch 调用四个接口的过程、"异步等待"是怎么回事、完整测试四个功能的结果和感受。完成后 git commit + push。

## 小白常见问题

- **Q：添加后列表没反应？** A：按 F12 看 Console 和 Network（网络）标签：请求是否发出、状态码是多少、后端是否在运行；把信息发来一起定位。
- **Q：出现跨域 / CORS 报错？** A：确认页面是从 http://localhost:3000 打开（而不是双击 index.html 用 file:// 方式打开），保持前后端同源即可。
- **Q：为什么操作后要重新 loadTodos？** A：数据库才是数据的"正本"，重新拉取能保证页面永远显示真实、最新的数据，避免前后端不一致。
