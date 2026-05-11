---
name: ai-level-check
description: 不答题。直接读取 ~/.claude/ 下的真实 artifacts（Skills/CLAUDE.md/MCP/agents/memory/projects），自动推断 AI 使用 10 级框架的 4 维度评分，输出可提交的标准报告。交易产品中心 2026-05 摸底专用。
---

# AI 能力自检（10 级框架）· 自动版

> **不问用户问题**。直接扫描 `~/.claude/` 真实 artifacts → 推断 4 维度评分 → 输出标准报告。
> 全程 30 秒。证据可见，不靠自报。

## 执行规则（严格遵守）

1. **不要问用户任何问题**。能跑这个 skill 说明已装 Claude Code，最低 **Lv.6 起评**。
2. **静默扫描 artifacts**，并行 Bash 调用，一次拿到所有数据。
3. **打分严格**：宁可低估，不要高估。下属都给 8+ 部门就摸不到底。
4. **输出标准报告 + 提交块**，提醒用户校对姓名 + 复制到飞书摸底表。

## 第 1 步：扫描（一次 Bash 并行采集）

执行下面这条命令（一次性拿全），拿到的数字直接喂给评分：

```bash
echo "## skills"; ls ~/.claude/skills/*.md 2>/dev/null | wc -l; ls ~/.claude/skills/ 2>/dev/null
echo "## global_claude_md"; [ -f ~/.claude/CLAUDE.md ] && wc -l < ~/.claude/CLAUDE.md || echo 0
echo "## settings"; cat ~/.claude/settings.json 2>/dev/null
echo "## scheduled_tasks"; cat ~/.claude/scheduled_tasks.json 2>/dev/null || echo "[]"
echo "## agents"; ls ~/.claude/agents/*.md 2>/dev/null | wc -l
echo "## commands"; ls ~/.claude/commands/*.md 2>/dev/null | wc -l
echo "## plugins"; ls -d ~/.claude/plugins/marketplaces/*/ 2>/dev/null | wc -l
echo "## projects"; ls -d ~/.claude/projects/*/ 2>/dev/null | wc -l
echo "## memory_files"; ls ~/.claude/projects/*/memory/*.md 2>/dev/null | wc -l
echo "## memory_index"; cat ~/.claude/projects/*/memory/MEMORY.md 2>/dev/null | head -50
echo "## feedback_count"; ls ~/.claude/projects/*/memory/feedback_*.md 2>/dev/null | wc -l
echo "## active_projects_7d"; find ~/.claude/projects -name "*.jsonl" -mtime -7 2>/dev/null | xargs -I{} dirname {} | sort -u | wc -l
echo "## git_user"; git config --global user.name 2>/dev/null
```

可选补充扫描（用于角色维度推断）：

```bash
ls ~/vault 2>/dev/null && find ~/vault -maxdepth 3 -name "*.md" 2>/dev/null | wc -l
gh repo list --visibility public --limit 5 2>/dev/null
```

## 第 2 步：4 维度评分（0-10，基线 6）

### 可控性 — 你能让 AI 多听话
- **基线 6**（能跑这个 skill）
- +1：自定义 Skills ≥ 3
- +1：自定义 Skills ≥ 8 **或** 全局 CLAUDE.md ≥ 50 行
- +1：MCP 服务器 ≥ 1 **或** hooks 已配置
- +1：feedback 记忆 ≥ 3（说明在持续调教 AI）
- 封顶 10
- 降级触发：没有全局 CLAUDE.md 且 skills < 3 → 直接降到 5（基础没打牢）

### 广度 — 覆盖多少场景
- **基线 6**
- +1：项目目录数 ≥ 5
- +1：项目目录数 ≥ 10
- +1：最近 7 天活跃项目 ≥ 3
- +1：memory 里有 personal/non-work 痕迹（看 project_*.md 是否有非工作类型如游戏/个人站等）
- 封顶 10
- 降级触发：项目目录 ≤ 1 → 降到 4

### 形态 — 协作复杂度
- **基线 6**（单 Agent 工具链熟练）
- +1：subagents ≥ 1 **或** custom commands ≥ 1
- +1：scheduled_tasks 非空 **或** hooks 已配置
- +1：subagents ≥ 2 **且** scheduled_tasks ≥ 1（多 Agent + 自动化）
- +1：发现完整自反馈机制（memory 体系 + feedback 文件 ≥ 5）
- 封顶 10
- 降级触发：仅 1 个项目 + 没有任何 agents/commands/scheduled → 降到 5

### 角色 — AI 在你认知中是什么（artifacts 推断版）
- **基线 6**（伙伴/同事）
- +1：MEMORY.md 体系完整（user-profile + feedback + project + reference 多类齐全）
- +1：有面向他人/教学型 Skills（README 型、含使用说明）
- +1：检测到 GitHub public 仓库分享方法论 **或** vault 里有 ≥ 20 个 .md 沉淀
- +1：memory 里有"影响他人"痕迹（project_*.md 提到分享/教学/团队推广）
- 封顶 10
- **重要**：角色维度从 artifacts 推断有局限（推不到工作外用法、线下影响力），结尾必须提醒用户在备注字段补充。

## 第 3 步：等级换算

平均分 → 等级：

| 平均 | 等级 |
|---|---|
| 6 | Lv.6 召唤师 |
| 7 | Lv.7 铸造师 |
| 8 | Lv.8 造物主 |
| 9 | Lv.9 觉醒者 |
| 10 | Lv.10 一人军团 |

**关键校准**：最低维 ≤ 4 → 整体降一级（短板比平均更说明问题）。

## 第 4 步：输出报告（按下面模板填）

```markdown
# AI 能力自检报告 · {{从 git config 或 memory user-profile 推断的姓名，无则写"请填写"}}

**日期**：{{今天 YYYY-MM-DD}}
**综合等级**：Lv.{{X}} {{称号}}
**评估方式**：基于本机 ~/.claude/ artifacts 自动推断（30秒扫描，无答题）

## 四维评分

| 维度 | 分数 | 关键证据（自动检测） |
|---|---|---|
| 可控性 | X/10 | 自定义 Skills X 个、CLAUDE.md X 行、MCP X 个、feedback 记忆 X 个 |
| 广度 | X/10 | 项目目录 X 个，最近 7 天活跃 X 个，{{有/无}}非工作类项目 |
| 形态 | X/10 | subagents X 个、commands X 个、scheduled_tasks X 个、hooks {{有/无}} |
| 角色 | X/10 | MEMORY 体系{{完整/部分/缺失}}、{{有/无}}对外分享 artifacts |

## 短板诊断
{{最低 1 维 + 1 个具体动作。例："形态最低（5/10），下周写 1 个 subagent 处理周报场景"}}

## 高光
{{最强 1 维。例："可控性 9/10，11 个自定义 Skills + 完整 memory 体系，是组里 Top 5%"}}

## 30 天进阶建议
{{1 条具体动作，不超过 3 句}}

---

## ⚠️ 角色维度局限说明

本报告角色维度仅基于本机 artifacts 推断，未覆盖：
- 工作外的 AI 使用（手机 ChatGPT、其他工具）
- 实际影响力（线下分享、内部文章、社群影响）

若有显著差异，请在提交块「备注」字段补充。

---

## 提交（必填）

直接复制下面表格 → 粘贴到飞书摸底表（链接由 Eason 在群里发）：

| 字段 | 值 |
|---|---|
| 姓名 | {{校对姓名}} |
| 综合等级 | Lv.{{X}} |
| 可控性 | X |
| 广度 | X |
| 形态 | X |
| 角色 | X |
| 短板 | （一句话） |
| 高光 | （一句话） |
| 30 天进阶动作 | （一句话） |
| 备注 | （选填，特别是角色维度补充） |
```

## 反作弊机制（自动版）

- **artifacts 是硬证据**，不靠自报
- 没法刷分：临时建几个空 Skill 文件 → 评分仍参考 CLAUDE.md 行数 / memory 体系完整度 / 项目活跃度等多个交叉信号
- 角色维度有局限 → 让用户备注字段补充，Eason 人工 review

## 完成提示

报告生成完毕后告诉用户：
1. 复制提交块到飞书摸底表
2. 校对姓名（自动推断不一定准）
3. 角色维度有补充 → 写到「备注」
4. 全程未问任何问题 → 数据全部来自本机 artifacts
