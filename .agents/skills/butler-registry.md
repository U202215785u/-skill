# 管家外部技能注册表

管家自己有一套内部角色。但用户可能装过更成熟的外部技能。
当 tool-scanner 检测到以下技能时，管家知道它们是什么、什么时候用、和内部角色怎么配合。

## 注册规则

- 外部技能比内部角色更好的场景 → 用外部的
- 外部技能和内部角色互补 → 同时激活
- 外部技能没有覆盖的场景 → 用内部的

---

## Superpowers 技能组

来源：`obra/superpowers`（通过 `npx skills add obra/superpowers` 安装）

| 技能 | 它做什么 | 什么时候用它 | 和内部角色的关系 |
|------|---------|------------|----------------|
| brainstorming | 探索需求、发散方案 | 用户说"我想做个XX但不知道怎么设计" | **比 product-manager 更好用**。但它只管发散，不管收敛成 PRD |
| writing-plans | 把需求写成可执行计划 | architect 出完方案后，需要拆成具体步骤时 | architect 管"设计什么"，writing-plans 管"怎么一步步做" |
| executing-plans | 按计划逐步执行 | 计划已写好，需要分步执行 | implementer 管"写代码"，executing-plans 管"按顺序执行多步" |
| tdd | 红-绿-重构循环，先写测试再写代码 | 用户要求高可靠性，或有回归风险 | Study-Hub 没有测试能力。**tdd 直接补了这个缺口** |
| debugging | 标准化调试流程 | 东西坏了需要系统排查 | **比 debugger 更成熟**。用 debugging 替代 debugger |
| verification | 做完后验证是否真的通过 | implementer 改完代码后 | auditor 管代码检查，verification 管功能验证。互补 |
| dispatching-parallel-agents | 无依赖任务并行分发 | 多个独立任务需要同时做 | Study-Hub 没有并行能力。**直接补缺口** |
| finishing-a-development-branch | 合入前检查、清理、PR | 功能做完准备合入 | caretaker 管健康，finishing 管分支收尾。互补 |
| requesting-code-review | 发起代码审查 | 需要第二意见 | auditor 管自动检查，requesting 管组织人工审查 |
| receiving-code-review | 处理审查反馈 | 收到 review 意见时 | Study-Hub 无此能力 |

## 激活优先级

当用户的问题同时命中内部角色和外部技能时：

1. **先查外部技能是否匹配。** 外部技能（尤其是 superpowers）经过了更大规模的验证。
2. **匹配到了 → 用外部的。** 但用管家的人类语言风格包装输出。
3. **外部没匹配到 → 用内部角色。**
4. **两者互补 → 同时激活。** 管家协调输入输出。

## 发现但未注册的技能

如果 tool-scanner 检测到用户装了其他不在本注册表的技能：
→ 读该技能的 SKILL.md，从描述中推断触发场景
→ 第一次激活时告诉用户"你装了一个能处理这个的，要我试试吗？"
→ 如果用户确认有效 → 记入 tool-experiences，下次直接用
