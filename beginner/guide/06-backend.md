# 第 6 步：第一个后端接口

> 本步目标：先实现"查、增"接口并用内存数据理解逻辑，再引入 SQLite 数据库实现数据持久化，补齐"改、删"接口，完成第 2 步设计的四个接口。

## 1. 进度（导师话术）

"这一步进'厨房'：先让后端能接收和返回待办数据，再把数据真正存进数据库，这样即使服务器重启，数据也不会丢。"

## 2. 为什么

- 接口是前后端的桥梁，后端负责处理逻辑、保证数据正确和安全。
- 内存里的数据一关程序就消失，数据库负责长期、可靠地保存，这是真实项目必须的一步。

## 3. 概念扫盲

- **中间件（middleware）**：请求到达处理逻辑前、先经过的一道道"关卡"。`express.json()` 这道关卡负责把前端发来的 JSON 数据解析成程序能用的对象。
- **req / res**：req（请求）装着前端发来的信息；res（响应）用来把结果发回去。
- **数据库**：专门存放和管理数据的软件。**SQLite** 是最轻巧的一种——整个数据库就是项目里的一个文件，不用单独安装服务器，非常适合入门和小项目。
- **SQL**：和数据库对话的语言，用"建表、插入、查询、更新、删除"等语句操作数据。

## 4. 跟着做

### （1）先让后端能读懂 JSON

在 server.js 顶部、路由前加：

```javascript
app.use(express.json());
```

### （2）先用内存数组实现"查"和"增"

```javascript
let todos = [];        // 临时存放，重启会清空
let nextId = 1;

app.get('/api/todos', (req, res) => {
  res.json(todos);     // 把全部待办以 JSON 返回
});

app.post('/api/todos', (req, res) => {
  const text = req.body.text;              // 取前端发来的内容
  if (!text || !text.trim()) {             // 校验：内容不能为空
    return res.status(400).json({ error: '内容不能为空' });
  }
  const todo = { id: nextId++, text: text.trim(), done: false };
  todos.push(todo);                       // 加入数组
  res.status(201).json(todo);             // 201 表示"创建成功"
});
```

解释：GET 返回列表；POST 先**校验输入**（空内容直接返回 400 错误，这是后端必须做的安全与正确性检查），再创建对象、保存并返回。

### （3）安装并接入 SQLite

```
npm install better-sqlite3
```

在 server.js 顶部引入并建表：

```javascript
const Database = require('better-sqlite3');
const db = new Database('data/todos.db');   // 数据库就是这个文件

db.exec(`
  CREATE TABLE IF NOT EXISTS todos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    text TEXT NOT NULL,
    done INTEGER NOT NULL DEFAULT 0,
    created_at TEXT DEFAULT (datetime('now'))
  );
`);
```

逐行解释 SQL 建表：`CREATE TABLE IF NOT EXISTS`（有就不重复建）；id 是主键且自动增长；text 不能为空；done 用 0/1 表示未完成/完成（数据库里布尔值常这样存）；created_at 默认取当前时间。字段与第 2 步设计完全对应。

### （4）用数据库重写四个接口

```javascript
// 查：获取全部待办
app.get('/api/todos', (req, res) => {
  const rows = db.prepare('SELECT * FROM todos ORDER BY id').all();
  const todos = rows.map(r => ({ id: r.id, text: r.text, done: r.done === 1 }));
  res.json(todos);
});

// 增：添加一条待办
app.post('/api/todos', (req, res) => {
  const text = req.body.text;
  if (!text || !text.trim()) {
    return res.status(400).json({ error: '内容不能为空' });
  }
  const info = db.prepare('INSERT INTO todos (text) VALUES (?)').run(text.trim());
  const todo = db.prepare('SELECT * FROM todos WHERE id = ?').get(info.lastInsertRowid);
  res.status(201).json({ id: todo.id, text: todo.text, done: todo.done === 1 });
});

// 改：切换完成状态
app.patch('/api/todos/:id', (req, res) => {
  const todo = db.prepare('SELECT * FROM todos WHERE id = ?').get(req.params.id);
  if (!todo) return res.status(404).json({ error: '找不到这条待办' });
  const newDone = todo.done === 1 ? 0 : 1;
  db.prepare('UPDATE todos SET done = ? WHERE id = ?').run(newDone, todo.id);
  res.json({ id: todo.id, text: todo.text, done: newDone === 1 });
});

// 删：删除一条待办
app.delete('/api/todos/:id', (req, res) => {
  const info = db.prepare('DELETE FROM todos WHERE id = ?').run(req.params.id);
  if (info.changes === 0) return res.status(404).json({ error: '找不到这条待办' });
  res.status(204).end();    // 204 表示成功但没有内容返回
});
```

讲解要点：
- `?` 是占位符，数据由 `.run()` 按位置填入，**永远这样传参而不要把用户输入拼进 SQL 语句**，能防止 SQL 注入（安全红线，用大白话解释：防止有人输入恶意内容篡改数据库）。
- SELECT 查询、INSERT 插入、UPDATE 更新、DELETE 删除正好对应 CRUD。
- 改、删操作先确认这条数据存在，不存在返回 404。
- 从数据库读出的 done 是 0/1，返回给前端前转成 true/false。

### （5）测试接口

- 浏览器访问 http://localhost:3000/api/todos 测试 GET（开始是空数组 []）。
- POST/PATCH/DELETE 用终端 curl 测试（PowerShell 用 curl.exe）：

```
curl.exe -X POST http://localhost:3000/api/todos -H "Content-Type: application/json" -d "{\"text\":\"第一条待办\"}"
```

完整的点击测试在第 7 步前端接入后直接在网页上进行。

## 5. 检查一下

让小白：①GET /api/todos 能返回数组；②用上面 curl 添加一条后再次 GET，能看到它；③停止服务器（Ctrl+C）再重新启动，数据依然在（证明数据库持久化生效）。

## 6. 学到了什么

1. 后端接口负责校验输入、处理逻辑、读写数据；空输入、找不到数据都要有明确错误响应。
2. 内存数据重启即失，数据库（SQLite）用一个文件持久保存数据。
3. SQL 的增删改查对应 CRUD；用占位符传参防止 SQL 注入是安全红线。

## 7. 记到项目文档

在 `PROJECT_JOURNAL.md` 记录：四个接口分别怎么实现、数据库表有哪些字段、"占位符防注入"是什么意思、重启后数据还在的验证结果。完成后 git commit。

## 小白常见问题

- **Q：better-sqlite3 安装报错？** A：确认 Node 是 LTS 版本并重试；个别环境需要编译工具，可换用纯 JS 的方案，把报错完整发来。
- **Q：POST 后 req.body 是空的？** A：确认已加 `app.use(express.json())`，且请求带了 `Content-Type: application/json` 头。
- **Q：data/todos.db 找不到或报错？** A：确认已创建 data 文件夹；该文件在第一次运行后自动生成。
