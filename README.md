# Study-Hub

**面向新手的 AI 项目协作操作系统。**

你不需要学 Claude。你只需要跟管家说话。管家替你做判断、替你用工具、替你写代码。搞错了能退。

---

## 这是什么

Study-Hub 不是一个 skill。它是一个**引导式协作协议**，套在高级 AI agent（如 Claude Code）外面。

核心就一件事：**一个完全不懂术语的人，打开终端，跟管家说话，管家帮他搞定一切。**

管家做的事：
- 听你说要什么（哪怕你说不清楚）
- 自己查项目状态、匹配工具、判断该做什么
- 动手前跟你确认（按风险分级，不说术语）
- 自己调工具、改代码、跑测试、失败了自己排查
- 把学到的经验记下来，下次更聪明

---

## 适合谁

**完全不会写代码的人。** 文科生、社科学者、独立创作者——任何被"AI 能写代码"吸引、但被终端和 bug 劝退的人。

**也适合装了 skill 但不知道什么时候用的人。** 你装了一堆 skill，但只会用自动触发的那几个。管家替你想起来"你装了一个能处理这个的"。

---

## 怎么装

1. 把这个仓库放到你项目的**根目录**：

```bash
git clone https://github.com/U202215785u/-skill.git study-hub
cp -r study-hub/* 你的项目目录/
```

2. 在 Claude Code 中打开项目。管家自动在线。

不需要触发词。打开终端，管家已经在等你了。

---

## 怎么验证跑通了

```bash
# 生成项目索引
cd 你的项目目录
python3 context/indexer.py
# 或 Windows: py -3 context/indexer.py

# 扫描已装工具
python3 context/tool-scanner.py
```

看到 `扫描完成：X 个文件` 就说明跑通了。

然后打开 Claude Code，说一句话试试：

> "帮我看看这个项目有什么问题"

管家会扫描你的项目，告诉你发现了什么。

---

## 项目结构

```
.
├── agent.md                          # 全局协议（自动加载）
├── README.md                         # 你正在看的
├── LICENSE                           # MIT
├── DEMO.md                           # 5 分钟演示场景
├── .agents/skills/
│   ├── butler.md                     # 管家核心层
│   ├── butler-init.md                # 初始化对话
│   ├── butler-guide.md               # 引导式排查
│   ├── butler-confirm.md             # 分级确认 + 撤销
│   ├── butler-debug-loop.md          # 三次尝试上限
│   ├── butler-error.md               # 错误处理
│   ├── butler-exit.md                # 退出 + 记忆回写
│   ├── butler-term-map.md            # 术语翻译
│   ├── product-manager.md            # 需求展开
│   ├── architect.md                  # 方案拆分
│   ├── implementer.md                # 写代码
│   ├── auditor.md                    # 代码检查
│   ├── debugger.md                   # 故障追踪
│   ├── caretaker.md                  # 健康巡检
│   ├── automation-expert.md          # ASR/ffmpeg/解析
│   ├── frontend-expert.md            # Vue/CSS/DOM
│   ├── backend-expert.md             # FastAPI/SQLite
│   └── visual-expert.md             # 配色/字体/UI
├── .agents/owners/                   # 领域知识库
├── context/
│   ├── indexer.py                    # 代码地图生成
│   └── tool-scanner.py               # 已装工具扫描
├── project-memory/
│   └── 项目索引.md                   # 管家唯一入口
└── user-memory.example/             # 用户级记忆模板
```

---

## 设计哲学

初始化只问一个顶层问题：

> "当我拿不准你具体想要什么的时候，你希望我怎么处理？"

用户的回答决定了管家的所有行为策略——是否自主执行、是否每次确认、说话精简还是详细。

其他一切从这个立场自动推导。

---

## 平台

Study-Hub 是**自定义协议文档**，兼容 Claude Code（通过 agent.md 自动加载）。Skill 文件为 .md 格式，内部使用。

不是标准的 Codex/Cursor skill 包——需要放到项目根目录手动使用。

---

## 许可

MIT
