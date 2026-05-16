---
name: douyin-project
description: |
  Project context for WorkBuddy Claw workspace. Contains Douyin account config, material library paths,
  publishing templates, and workspace environment settings.
  Activate when user mentions: 抖音/【你的账号名】/自媒体/视频/发布/素材库/模板/账号运营.
agent_created: true
---

# 工作区上下文（自媒体版）

## Quick Reference Index
| Domain | Detail Location |
|--------|----------------|
| 抖音账号配置 | `references/project-config.md` → Douyin Section |
| 素材库路径 | `references/project-config.md` → Material Library |
| 运营模板包 | `references/project-config.md` → Templates |
| 系统环境 | `references/project-config.md` → System Section |

## Progressive Disclosure Rules
1. This SKILL.md (~20 lines) loads on trigger — minimal token cost
2. Read `references/project-config.md` only when task needs specific config
3. For script writing tasks: load Material Library + Templates sections
4. For publishing tasks: load Douyin Account + Schedule sections
5. Never load full file unless cross-domain work is needed
