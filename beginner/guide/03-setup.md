# 第 3 步：搭建项目——安装环境、初始化项目

> 本步目标：建立项目文件夹和标准结构，初始化 Node 项目，安装 Express，并写出一个能在浏览器访问的最简单后端。

## 1. 进度（导师话术）

"图纸有了，这一步我们正式'动工'：先把项目的'地基和房间'搭好，让一个最简单的网页能在你电脑上跑起来。"

## 2. 为什么

- 规范的目录结构让代码各归其位，项目变大也不会乱。
- 先跑通一个最简单的版本（哪怕只显示一句话），能确认环境没问题，再往上加功能就有底气——这叫"先让骨架活起来"。

## 3. 概念扫盲

- **package.json**：项目的"身份证 + 账本"，记录项目名字、用到哪些别人的工具（依赖）、有哪些命令。
- **依赖（库）**：别人写好、我们借来用的现成工具。**Express** 就是一个专门用来快速搭建后端服务器的库。
- **node_modules/**：下载下来的所有依赖存放的文件夹，体积大、由 npm 管理，**不需要也不应该自己存档**。
- **localhost:3000**：你自己这台电脑上的"3000 号门"。服务器启动后，浏览器访问这个地址就能敲开它。localhost 永远指"本机"。
- **.gitignore**：一张"忽略清单"，列在里面的文件 Git 不会存档（比如 node_modules）。

## 4. 跟着做

### （1）建项目文件夹并用 VS Code 打开

在你找得到的地方（如文档目录）新建文件夹 `todo-app`。打开 VS Code → `文件 → 打开文件夹` 选中它。然后 `终端 → 新建终端`，确认终端路径就在这个文件夹里。

### （2）初始化 Node 项目

在终端输入：

```
npm init -y
```

解释：`npm init` 用来生成 package.json，`-y` 表示"全部用默认值"，先快速生成，之后可以打开 package.json 改描述。

### （3）安装 Express

```
npm install express
```

解释：这一步会从 npm 下载 Express，自动出现 node_modules 文件夹，并在 package.json 里记下"本项目依赖 express"。同时生成的 package-lock.json 用来精确锁定版本，保证以后重装结果一致。

### （4）建立目录结构

在 VS Code 里新建如下文件和文件夹：

```
todo-app/
├── public/          # 放前端文件（网页、样式、脚本）
│   └── （第 5 步使用）
├── data/            # 放数据库文件（第 6 步之后使用）
├── server.js        # 后端主程序
└── package.json     # 已由 npm init 生成
```

### （5）写最简单的后端

在 `server.js` 里输入：

```javascript
const express = require('express');   // 引入别人做好的 Express 工具
const app = express();                // 创建一个服务器应用
const PORT = 3000;                    // 约定使用 3000 号门

app.get('/', (req, res) => {          // 当有人访问首页 "/" 时
  res.send('我的待办清单服务器跑起来了！');  // 回复一句话
});

app.listen(PORT, () => {              // 启动服务器，开始监听 3000 号门
  console.log('服务器已启动：http://localhost:' + PORT);
});
```

逐行解释见行内注释。核心三件事：引入工具 → 定义"访问某地址时回什么"→ 启动监听。

### （6）运行

```
node server.js
```

然后打开浏览器，地址栏输入 `http://localhost:3000`，应看到"我的待办清单服务器跑起来了！"。
停止服务器：在终端里按 `Ctrl + C`。

### （7）创建 .gitignore

在项目根目录新建 `.gitignore`，写入：

```
node_modules/
data/*.db
.env
```

解释：node_modules 体积大且能用 package.json 重新下载，不存档；数据库文件和含密码的配置也不存档。

（可选，推荐）安装自动重启工具：`npm install --save-dev nodemon`，之后用 `npx nodemon server.js` 启动，每次保存代码会自动重启，省去手动停止再运行。

## 5. 检查一下

让小白截图浏览器页面（显示那句话）和终端（显示"服务器已启动"）。能看到页面 = 后端环境完全跑通。

## 6. 学到了什么

1. package.json 是项目账本，node_modules 是依赖目录且不存档。
2. Express 让我们用几行代码搭起服务器；服务器的本质是"一直运行、等待请求并给出响应"。
3. localhost:3000 是访问本机服务器的地址；先跑通最小骨架是重要的开发习惯。

## 7. 记到项目文档

在 `PROJECT_JOURNAL.md` 记录：项目目录结构、安装了哪些依赖、server.js 每行大概做什么、第一次在浏览器看到自己服务器的结果。

## 小白常见问题

- **Q：终端提示 "require is not defined" 或报错？** A：确认是用 `node server.js` 运行（而不是把代码放进浏览器），并确认在项目根目录、已成功 `npm install express`。
- **Q：端口 3000 "被占用"怎么办？** A：把代码里和访问地址中的 3000 改成 3001 等其他数字即可。
- **Q：改了 server.js 为什么页面没变？** A：用 node 运行需要停止（Ctrl+C）后重新 `node server.js`；用上面的 nodemon 则会自动重启。
