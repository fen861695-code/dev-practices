# 第 5 步：第一个前端页面

> 本步目标：理解 HTML/CSS/JavaScript 各管什么，写出待办清单的页面结构、样式和交互骨架，并让 Express 能把这个网页发给浏览器。

## 1. 进度（导师话术）

"这一步我们装修'大堂'，做用户看得见、点得到的页面。你会第一次在浏览器里看到自己亲手做的待办清单界面。"

## 2. 为什么

- 前端是用户的全部体验，页面结构清晰、交互顺畅，产品才好用。
- 先把页面和交互骨架做出来（先用几条假数据），第 7 步再把它和后端真数据连起来，分步走更容易成功。

## 3. 概念扫盲（盖房子类比）

- **HTML**：房子的结构——墙、门、窗在哪里。负责"页面上有什么"。
- **CSS**：装修和软装——颜色、大小、间距、好不好看。负责"长什么样"。
- **JavaScript（JS）**：水电和开关——按按钮会发生什么、内容如何变化。负责"能做什么"。
- **DOM**：浏览器把网页整理成的一棵"家谱树"，JS 通过它来读取和修改页面上的内容。
- **静态文件**：HTML/CSS/图片这类内容固定、直接发给浏览器的文件，需要让服务器知道去哪取。

## 4. 跟着做

### （1）让 Express 托管前端文件

在 `server.js` 里、路由之前加一行：

```javascript
app.use(express.static('public'));
```

解释：告诉服务器"public 文件夹里的文件直接发给浏览器"。这样访问 http://localhost:3000 时会自动返回 public/index.html。

### （2）写页面结构 public/index.html

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>我的待办清单</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>我的待办清单</h1>

  <div class="input-area">
    <input id="todo-input" type="text" placeholder="输入一条待办……">
    <button id="add-btn">添加</button>
  </div>

  <ul id="todo-list"></ul>

  <script src="app.js"></script>
</body>
</html>
```

解释关键标签：`input` 是输入框（id 让 JS 能找到它）；`button` 是按钮；`ul` 是无序列表，待办会由 JS 动态填进去；最后引入样式表和脚本。

### （3）写样式 public/style.css

```css
body {
  font-family: sans-serif;
  max-width: 480px;
  margin: 40px auto;
  padding: 0 16px;
}
.input-area { display: flex; gap: 8px; }
#todo-input { flex: 1; padding: 8px; }
.todo-item { display: flex; align-items: center; gap: 8px; margin: 8px 0; }
.todo-item.done .text { text-decoration: line-through; color: #999; }
.delete-btn { margin-left: auto; }
```

解释：CSS 通过标签名、#id、.class 找到元素并设置外观；`.todo-item.done .text` 表示"已完成条目里的文字"加删除线，这正是第 2 步设计的效果。

### （4）写交互骨架 public/app.js（先用假数据）

```javascript
// 先用假数据让页面动起来，第 7 步换成从后端获取
let todos = [
  { id: 1, text: '学习 HTML', done: true },
  { id: 2, text: '学习 CSS', done: false }
];

const todoList = document.getElementById('todo-list');

function render() {
  todoList.innerHTML = '';                  // 先清空列表
  todos.forEach(function (todo) {           // 遍历每条待办
    const li = document.createElement('li');      // 创建一个 <li>
    li.className = 'todo-item' + (todo.done ? ' done' : '');

    const checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.checked = todo.done;

    const span = document.createElement('span');
    span.className = 'text';
    span.textContent = todo.text;           // textContent 安全地设置文字

    const delBtn = document.createElement('button');
    delBtn.className = 'delete-btn';
    delBtn.textContent = '删除';

    li.appendChild(checkbox);
    li.appendChild(span);
    li.appendChild(delBtn);
    todoList.appendChild(li);
  });
}

render();   // 页面加载时先画一次
```

解释：这是操作 DOM 的典型过程——先 createElement 造元素、设置内容和样式，再 appendChild 拼到页面上；`render()` 根据数据重新画出整个列表，以后数据一变只要重新调用它。强调 `textContent` 而不是直接拼 HTML，能防止恶意内容被当成标签执行（安全习惯）。

按钮的点击逻辑（添加、勾选、删除）在第 7 步连同后端数据一起实现，本步先看到列表。

## 5. 检查一下

重启/确认服务器运行，浏览器访问 http://localhost:3000，应看到标题、输入框、添加按钮，以及两条假待办（第一条带删除线）。让小白截图核对。

## 6. 学到了什么

1. HTML 管结构、CSS 管外观、JS 管交互，三者分工协作。
2. JS 通过 DOM 读取和修改网页；"根据数据用 render() 重新画页面"是前端的核心思路。
3. express.static 让服务器把 public 里的前端文件发给浏览器。

## 7. 记到项目文档

在 `PROJECT_JOURNAL.md` 记录：HTML/CSS/JS 各负责什么、render 函数怎么把数据变成页面、看到第一个页面的效果。完成后做一次 git commit。

## 小白常见问题

- **Q：页面没有样式或脚本没生效？** A：检查 index.html 里 link/script 的文件名是否与实际一致（注意大小写），并确认文件都在 public 目录、服务器已用 static 托管。
- **Q：为什么列表是空的？** A：确认 app.js 末尾调用了 `render()`，并按 F12 打开浏览器控制台查看是否有红色报错，把报错发来。
