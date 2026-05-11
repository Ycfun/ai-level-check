# 交易产品中心 · AI 能力摸底（1 分钟自检）

> 各位，我们做一次全员 AI 水位摸底。**不是考核**，是为了找到团队拐点和共性短板，决定下一步教练资源往哪投。
> Deadline：**2026-05-18**（一周）

---

## 怎么做（3 步，1 分钟）

### 1. 装 Skill

打开 Claude Code，跑：

```bash
git clone https://github.com/Ycfun/ai-level-check.git ~/.claude/skills/ai-level-check
```

### 2. 跑自检

在 Claude Code 里输入：

```
/ai-level-check
```

它会**静默扫描**你机器上的 `~/.claude/` artifacts（Skills / CLAUDE.md / MCP / memory / projects 等），30 秒出报告。**不会问你任何问题**。

### 3. 提交

报告末尾有一个**提交块**（表格形式）：

1. 校对自动推断的姓名
2. 角色维度有补充（工作外 AI 使用、线下分享、带教等）→ 写到「备注」
3. 整块复制 → 粘贴到摸底表：

> 📋 **摸底表**：https://futu.feishu.cn/base/H1zSbfwdba7ixcsDHO2cznMJnUU

---

## 评什么（4 维度 · 各 0-10 分）

| 维度 | 大白话 | 检测什么 |
|---|---|---|
| **可控性** | 你能让 AI 多听话 | Skills 数 / CLAUDE.md / MCP / feedback 记忆 |
| **广度** | 覆盖多少场景 | projects 数 / 7 天活跃 / 是否有非工作项目 |
| **形态** | 协作复杂度 | subagents / commands / scheduled / hooks |
| **角色** | AI 在你认知中是什么 | memory 体系 / 教学型 Skills / 对外分享 |

**基线 Lv.6**（能跑这个 skill 就达到了）。综合等级 = 4 维平均分向下取整。

---

## 几个常问

**Q：评得低怕被看到？**
A：摸底不是考核。低不可怕，看到自己短板比给自己打 8 分更有用。我会用结果反向投资源，不是用来打分。

**Q：跑出来比我自评低？**
A：Skill 故意调严格——下属都给 8+ 我就摸不到底了。觉得明显不对在「备注」写一句，我人工 review。

**Q：能用 ChatGPT 自评吗？**
A：不行，必须读 `~/.claude/` 的 Claude Code artifacts，换工具结果不可比。

**Q：能不交吗？**
A：30 人有一个不交我就摸不到底。有意见先跑完再提，比拒答有用。

---

## 详细版

需要更详细的框架说明、10 级速查、字段释义 → 看 [GUIDE.md](https://github.com/Ycfun/ai-level-check/blob/main/GUIDE.md)

任何问题群里直接 @我。
