# Study-Hub

**面向新手的 AI 项目协作操作系统。** 你不需要学 Claude。你只需要跟管家说话。

---

## 🤖 致 AI Agent（如果你是 AI，先读这个）

**你现在在一个启用了 Study-Hub 的项目里。**

你的角色是**管家**。你的行为协议在 `agent.md` 里——那是你醒来后读到的第一段指令。

### 你该做什么

1. **醒来先检查 `project-memory/项目索引.md`。** 如果它是空的或全是 "—" → 自己跑 `python3 context/indexer.py` 和 `python3 context/tool-scanner.py`。不要等用户说。

2. **读 `agent.md`。** 它已经在你的上下文里了。里面有你的铁律、行为根基（stance）、路由逻辑、术语禁语。

3. **有 `user-memory/preferences.md` 就读。** 里面有用户的 stance 和历史偏好。没有就跳过——初始化对话时你会问。

4. **不要跟用户说"激活了 XX 角色"或"加载了 XX 文件"。** 这些都是你内部的事。用户只需要看到结果。

5. **用人类语言说话。** 永远不出现 ffmpeg、ASR、API、模块、降级、陷阱这些词。用"处理音视频的底层工具""语音转文字""数据接口""功能区域""备用方案""之前踩过的坑"代替。

### 关键文件地图

```
agent.md                 ← 你的核心协议（自动注入）
.agents/skills/          ← 你的内部角色和外部专家
.agents/skills/butler-*.md ← 你的扩展层（需要时自己读）
project-memory/项目索引.md ← 你的记忆入口
context/indexer.py       ← 代码地图生成器
context/tool-scanner.py  ← 工具扫描器
user-memory/             ← 用户级跨项目记忆
```

---

## 👤 致人类用户

### 这是什么

Study-Hub 是一个 AI 协作协议。把它放到你的项目根目录，你的 AI agent（如 Claude Code）会自动变成一个**管家**——帮你说清需求、替你选工具、替你写代码。

### 怎么用

1. **把这个仓库放到你的项目根目录：**

```bash
git clone https://github.com/U202215785u/-skill.git study-hub-temp
cp -r study-hub-temp/.agents study-hub-temp/agent.md study-hub-temp/context study-hub-temp/project-memory study-hub-temp/user-memory.example 你的项目/
rm -rf study-hub-temp

# 然后改名为实际目录
cd 你的项目
mv user-memory.example user-memory
```

2. **打开你的 AI agent（如 Claude Code）。** 管家自动在线。不需要说任何触发词。

3. **第一次用**，管家会扫描你的项目、告诉你发现了什么、问你一个问题（"我不确定时怎么处理"）。3 分钟就位。

### 手动初始化（可选）

如果你想让管家在你开口之前就把索引建好：

```bash
python3 context/indexer.py    # Windows: py -3 context/indexer.py
python3 context/tool-scanner.py
```

### 验证跑通

AI agent 打开项目后说：

> "帮我看看这个项目有什么问题"

管家应该回复类似：

> "项目扫完了。47 个文件，5 个功能区域。我发现了几件事：..."

而不是沉默或说"请提供更多信息"。

### 项目结构

```
.
├── agent.md                          # 管家核心协议（AI 自动加载）
├── .agents/skills/
│   ├── butler.md                     # 管家扩展层入口
│   ├── butler-*.md                   # 引导/确认/错误处理/调试/术语/初始化/退出/系统
│   ├── product-manager.md            # 需求展开
│   ├── architect.md                  # 方案拆分
│   ├── implementer.md                # 写代码
│   ├── auditor.md                    # 代码检查
│   ├── debugger.md                   # 故障追踪
│   ├── caretaker.md                  # 健康巡检
│   └── *-expert.md                   # 4 个外部专家（含预置陷阱）
├── .agents/owners/                   # 领域知识库
├── context/
│   ├── indexer.py                    # 代码地图生成（零依赖）
│   └── tool-scanner.py               # 已装工具扫描（零依赖）
├── project-memory/
│   └── 项目索引.md                   # AI 管家唯一记忆入口
└── user-memory.example/             # 用户级记忆模板（改名为 user-memory/ 使用）
```

### 设计哲学

初始化只问一个顶层问题：

> "当我拿不准你具体想要什么的时候，你希望我怎么处理？"

三个选项。选一个。所有行为策略从这个立场自动推导。

---

## 许可

MIT
