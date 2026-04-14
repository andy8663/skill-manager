---
name: skill-manager
description: OpenClaw Skill 管理工具集：安装/卸载/更新/检查/搜索。触发词：查看技能列表/Skill管理/更新技能/卸载技能/搜索技能。自动识别来源（GitHub/SkillHub/Config/Local），一键升级。
version: "1.0.0"
homepage: https://github.com/andy8663/skill-manager
metadata:
  openclaw:
    emoji: "🛠️"
    category: "system"
    requires:
      bins: ["python3"]
---

# Skill Manager

> 统一管理 OpenClaw 已安装 Skills：查看列表、检查更新、升级、卸载。

## 功能

- **list** — 扫描 `~/.qclaw/workspace/skills` 和 `~/.qclaw/skills`，列出所有 Skill（名称/版本/来源/路径）
- **check** — Dry Run 检查所有 Skill 是否有更新，打印各来源对应的升级命令
- **update** — 从对应来源升级指定 Skill（GitHub → `git pull`，SkillHub → `skillhub install`）
- **uninstall** — 卸载指定 Skill（需确认，支持 `-y` 跳过确认）

## 来源分类

| 来源 | 说明 | 更新方式 |
|------|------|----------|
| **GitHub** | 有 `.git` 目录，从 GitHub 克隆的 Skill | `git pull` |
| **SkillHub** | 有 `_meta.json` 文件，从 SkillHub 安装 | `skillhub install <slug>` |
| **Config** | 有 `config.json` 文件，QClaw 内置 Skill | 随 QClaw 版本更新 |
| **Local** | 其他本地 Skill | 无自动更新路径 |

## 使用方式

```
python scripts/skill_manager.py list
python scripts/skill_manager.py check
python scripts/skill_manager.py update <name>
python scripts/skill_manager.py uninstall <name> [-y]
```

## 示例

```bash
# 查看所有 Skill
python scripts/skill_manager.py list

# 检查哪些可以更新（Dry Run）
python scripts/skill_manager.py check

# 更新某个 Skill
python scripts/skill_manager.py update wechat-oa

# 卸载（会提示确认）
python scripts/skill_manager.py uninstall some-old-skill

# 卸载（跳过确认）
python scripts/skill_manager.py uninstall some-old-skill -y
```

## 来源判断逻辑

1. Skill 目录下有 `.git` → **GitHub**
2. 有 `_meta.json` → **SkillHub**（联网查 ClawHub 最新版本）
3. 有 `config.json` → **Config**
4. 其他 → **Local**
