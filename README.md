# ai-level-check

> 交易产品中心 · AI 能力自检 Skill（10 级框架 · 自动版）
> Claude Code 专用，**不答题**，扫描本机 artifacts → 自动评 4 维度（可控性 / 广度 / 形态 / 角色）→ 输出可提交报告。

## 一分钟安装

```bash
mkdir -p ~/.claude/skills/ai-level-check
curl -fsSL https://raw.githubusercontent.com/Ycfun/ai-level-check/main/SKILL.md \
  -o ~/.claude/skills/ai-level-check/SKILL.md
```

或直接 `git clone`：

```bash
git clone https://github.com/Ycfun/ai-level-check.git ~/.claude/skills/ai-level-check
```

## 怎么用

1. 在任意项目里打开 Claude Code
2. 输入 `/ai-level-check`
3. **不会问你任何问题**，30 秒静默扫描 `~/.claude/` 下的真实 artifacts（Skills/CLAUDE.md/MCP/agents/memory/projects 等）
4. 拿到报告后，把"提交块"粘贴到飞书摸底表（链接由 Eason 在群里发）

## 框架来源

「AI 使用 10 级」框架，从 4 个维度自动评分（基线 6 起）：

- **可控性** —— 你能让 AI 多听话（看 Skills 数 / CLAUDE.md / MCP / feedback 记忆）
- **广度** —— 覆盖多少场景（看 projects 目录数 / 7 天活跃数 / 个人非工作项目）
- **形态** —— 协作复杂度（看 subagents / commands / scheduled_tasks / hooks）
- **角色** —— AI 在你认知中是什么（看 memory 体系完整度 / 对外分享 artifacts）

详见 [SKILL.md](./SKILL.md)。

## 反作弊

- **artifacts 是硬证据**，不靠自报，没法刷分
- 角色维度从 artifacts 推断有局限（推不到工作外用法、线下影响力）→ 报告里会提醒在备注字段补充
- Eason 人工 review 备注

## License

Internal use · 交易产品中心
