# 抖音创作者 Skill 套件

> 一套完整的抖音短视频内容创作 AI 工作流，从选题调研到数据复盘，13 个专业 Skill 覆盖全流程。
> 适用于 [WorkBuddy / CodeBuddy](https://www.codebuddy.cn/) 平台。

---

## 🎯 这是什么？

这套 Skill 把抖音短视频内容创作拆成了一条**可复用的流水线**：

```
选题研究 → 文案生成 → 双盲评分 → 方案生成 → 拍摄发布 → 数据复盘 → 账号规划
```

每个环节都有独立的 Skill 负责，同时有一个 **Orchestrator** 协调整条流水线自动化运行。

---

## 📦 Skill 清单（13 个）

| # | Skill | 职责 | 独立使用 |
|:-:|:------|:-----|:--------:|
| 1 | **douyin-orchestrator** | 多 Agent 协同流水线，一键启动全流程 | ✅ |
| 2 | **douyin-topic-research** | 选题调研 + 7 关否决制 + 钩子生成 | ✅ |
| 3 | **douyin-script-writing** | 口播逐字稿生成 + 品类适配结构 | ✅ |
| 4 | **douyin-script-scoring** | A/B/C/D 四类评分 + 双盲评审 + 否决制 | ✅ |
| 5 | **douyin-plan-generator** | 方案组装 + 预尸检 + 标题/标签/BGM | ✅ |
| 6 | **douyin-view-prediction** | 播放量预测 + 冷启动修正 + 概率分布 | ✅ |
| 7 | **douyin-data-review** | 数据复盘 + 偏差根因 + 校准触发 | ✅ |
| 8 | **douyin-account-review** | 账号层面复盘 + 阶段判断 + 合集规划 | ✅ |
| 9 | **douyin-workstyle** | 创作者人设/语速/禁用词/发布时间定义 | ✅ |
| 10 | **douyin-status** | 状态看板（只读），Buffer/校准/待办 | ✅ |
| 11 | **douyin-research** | 通用调研（纵横分析法 + 专家路由） | ✅ |
| 12 | **douyin-project** | 项目上下文配置（渐进式加载） | ✅ |
| 13 | **douyin-longvideo-scoring** | 长视频评分路由（→ script-scoring） | ✅ |

---

## 🏗️ 架构

```
┌─────────────────────────────────────────────────┐
│              douyin-orchestrator                  │
│         （自动模式 / 手动模式）                    │
├──────────┬──────────┬──────────┬────────────────┤
│ 阶段1    │ 阶段2    │ 阶段3    │ 阶段4           │
│ 选题研究  │ 文案生成  │ 双盲评分  │ 方案生成        │
│          │          │          │                │
│ topic-   │ script-  │ script-  │ plan-          │
│ research │ writing  │ scoring  │ generator      │
│          │          │ (A+B独立) │                │
├──────────┴──────────┴──────────┴────────────────┤
│ 阶段5: 数据复盘 (T+3天)  │ 阶段6: 账号复盘      │
│ data-review              │ account-review       │
└─────────────────────────────────────────────────┘
         ▲                    ▲
         │                    │
    douyin-workstyle    douyin-status
    (人设/语速/规则)    (只读看板)
```

---

## ⚡ 安装

### 前置条件

- 已安装 [WorkBuddy Desktop](https://www.codebuddy.cn/) 或 CodeBuddy Code
- 已登录并激活 AI 对话功能

### 方式一：Git 仓库导入（推荐）

1. 打开 WorkBuddy → **设置 → 技能管理 → 导入技能**
2. 选择 **从 Git 仓库导入**
3. 粘贴仓库地址：`https://github.com/chenxkj/laochen`
4. 确认导入，等待自动拉取完成

### 方式二：手动安装

**Windows (PowerShell)：**

```powershell
# 克隆仓库
git clone https://github.com/chenxkj/laochen.git

# 复制到用户级 skills 目录（所有项目可用）
Copy-Item -Recurse -Path "laochen\skills\*" -Destination "$env:USERPROFILE\.workbuddy\skills\"
```

**macOS / Linux：**

```bash
git clone https://github.com/chenxkj/laochen.git
cp -r laochen/skills/* ~/.workbuddy/skills/
```

> **路径说明**：
> - 用户级（所有项目可用）：`~/.workbuddy/skills/`
> - 项目级（仅当前项目）：`你的项目目录/.workbuddy/skills/`
> - CodeBuddy IDE 用户：`~/.codebuddy/skills/`

### 方式三：拖拽导入

将 `skills/` 下的任意 Skill 文件夹直接拖入 WorkBuddy 主窗口，松手即自动导入。

---

## 🔧 配置（安装后必做）

> 📖 完整配置图文指引见 [SETUP.md](SETUP.md)

安装后需要完成 3 步配置才能正常使用：

### 1. 设置人设信息

编辑 `douyin-workstyle/SKILL.md`，将占位符替换为你的实际信息：

| 占位符 | 替换为 | 示例 |
|:------|:------|:-----|
| `【N年XX经验】` | 你的从业年限和领域 | 8年产品经理 |
| `【你的学校/背景】` | 你的学历背景 | 浙大毕业 |
| `【你的昵称】` | 你的视频昵称 | 阿杰 |
| `【你的账号名】` | 你的抖音账号名 | 阿杰说产品 |

### 2. 设置项目配置

编辑 `douyin-project/references/project-config.md`，填入你的账号信息和本地路径。

### 3. 初始化状态文件

在你的项目根目录创建 `.cheat-state.json`（内容见 [SETUP.md](SETUP.md)）。

### 验证安装

在 WorkBuddy 对话中输入：

```
状态
```

如果看到状态看板输出，说明安装成功！

---

## 🚀 使用方式

### 全流程（推荐新手）

```
开始制作新视频·主题是"面试时被问到缺点怎么说"
```

Orchestrator 会自动协调全流程：选题研究 → 写稿 → 双盲评分 → 生成方案。

### 单步使用

| 你想做什么 | 输入 |
|:---------|:-----|
| 选题评估 | `研究一下"XX方向"行不行` |
| 写稿 | `写稿·主题是XXX` |
| 评分 | `评分`（然后上传稿子文件） |
| 生成方案 | `生成方案` |
| 预测播放量 | `预测一下` |
| 数据复盘 | `做复盘`（然后上传数据截图） |
| 账号复盘 | `账号复盘` |
| 查看状态 | `状态` |

---

## 📐 核心方法论

### A/B/C/D 四类评分体系

| 类 | 时长 | 字数 | 门槛 | 核心考核 |
|:--:|:----:|:----:|:----:|:--------|
| A | ≤1min | ≤279字 | ≥90 | 前3秒流失 + 完播率 |
| B | 1-3min | 279-843字 | ≥90 | 15秒停留 + 收藏 + 分享 |
| C | 3-5min | 843-1404字 | ≥90 | 留存曲线 + 评论 + 关注 |
| D | ≥5min | ≥1404字 | ≥90 | 复看 + 收藏 + 长尾 |

### 双盲评审机制

评分必须由**两个独立 Agent** 在不同会话中执行，互不可见：
- 差值 ≤ 10分 → 取平均分
- 差值 > 10分 → 触发第三人仲裁，取中位数

### 预尸检（Plan for Failure）

方案生成前必须回答4个问题：如果这条视频失败了，可能是什么原因？——把复盘前移到拍之前。

### 校准循环

```
盲预测 → 发布 → T+3天复盘 → 偏差分析 → 修正评分公式 → 更准确的预测
```

---

## 📁 目录结构

```
skills/
├── douyin-account-review/SKILL.md
├── douyin-data-review/SKILL.md
├── douyin-longvideo-scoring/SKILL.md
├── douyin-orchestrator/SKILL.md
├── douyin-plan-generator/
│   ├── SKILL.md
│   └── references/标题公式库.md
├── douyin-project/
│   ├── SKILL.md
│   └── references/
│       ├── project-config.md
│       └── state-schema.md
├── douyin-research/SKILL.md
├── douyin-script-scoring/
│   ├── SKILL.md
│   └── references/
│       ├── calibration-tools.md
│       ├── category-benchmarks.md
│       ├── fg-dimension.md
│       ├── historical-data.md
│       ├── red-lines.md
│       ├── ts-ms-guide.md
│       └── version-history.md
├── douyin-script-writing/
│   ├── SKILL.md
│   └── references/钩子库.md
├── douyin-status/SKILL.md
├── douyin-topic-research/SKILL.md
├── douyin-view-prediction/SKILL.md
└── douyin-workstyle/SKILL.md
```

---

## 🤝 适用场景

- **抖音短视频创作者**：从0到1搭建内容生产流程
- **职场/知识类博主**：人设驱动+故事优先的创作方法论
- **自媒体团队**：用AI辅助选题-写稿-评分-复盘的标准化流程
- **AI工作流研究者**：多Agent协同、双盲评审、校准循环的实践案例

---

## ❓ 常见问题

**Q：安装后对话中没看到这些 Skill？**
A：重启 WorkBuddy 或在设置中刷新技能列表。确认 Skill 文件夹放在正确路径下且包含 `SKILL.md` 文件。

**Q：评分和写稿在同一个会话里行不行？**
A：不行。双盲评分必须在**独立会话**中执行，否则评分会受写稿过程影响，失去校准价值。

**Q：我没有历史视频数据怎么办？**
A：不影响使用。`historical-data.md` 里的模板数据可以留着，等你发布3条以上视频后替换为真实数据，评分和预测会更准确。

**Q：能只装其中几个 Skill 吗？**
A：可以，每个 Skill 都能独立使用。但 Orchestrator 全流程需要所有核心 Skill 都已安装。

---

## ⚠️ 注意事项

1. **必须配置人设**：安装后务必修改 `douyin-workstyle` 和 `douyin-project` 中的占位符
2. **评分需独立会话**：双盲评分必须在独立 Agent 会话中执行，不能在写稿同一会话中评分
3. **数据复盘要数据先行**：复盘时先读数据文件，最后读稿子，避免后视偏差
4. **历史数据模板**：`historical-data.md` 中的数据是模板格式，请替换为你自己的实际数据

---

## 📜 License

MIT License - 自由使用、修改和分发。

---

## 🙏 致谢

本套件基于 cheat-on-content 校准体系思想，融合了实战运营经验，适配中文抖音创作场景。
