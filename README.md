# ai-level-check

> 交易产品中心 · AI 能力自检 Skill（10 级框架）
> 适用于 Claude Code，4 维度（可控性 / 广度 / 形态 / 角色）摸底，输出可提交报告。

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
3. 跟着 4 轮问题回答（每轮 3 题，全程 ~10 分钟）
4. 拿到报告后，把"提交块"粘贴到飞书摸底表

## 框架来源

「AI 使用 10 级」框架，从 4 个维度评分：
- **可控性** —— 你能让 AI 多听话
- **广度** —— 覆盖多少场景
- **形态** —— 协作复杂度
- **角色** —— AI 在你认知中是什么

详见 [SKILL.md](./SKILL.md)。

## 反作弊

- 自报数字不算，必须举具体例子
- 含糊回答追问 1 次再打分
- 短板维度（≤4）整体降一级

## License

Internal use · 交易产品中心
