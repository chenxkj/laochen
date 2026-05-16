# 配置指南

安装 Skill 套件后，必须完成以下配置才能正常使用。

---

## 第一步：配置人设（必做）

编辑 `douyin-workstyle/SKILL.md`，搜索并替换以下占位符：

| 占位符 | 你的实际信息 | 示例 |
|:------|:----------|:-----|
| `【N年XX经验】` | 从业年限+领域 | 10年UI设计 |
| `【你的学校/背景】` | 学历背景 | 美院毕业 |
| `【你的年龄】` | 年龄 | 30岁 |
| `【N人团队】` | 团队规模 | 8人团队 |
| `【你的昵称】` | 视频昵称 | 小王 |
| `【你的账号名】` | 抖音号名称 | 小王聊设计 |
| `【你的内容方向】` | 内容定位关键词 | 聊职场 / 设计思维 / 转型实录 |

### 人设锚点示例

原文：
```
- 【N年XX经验】老兵，研发总监，【你的学校/背景】出身
```

替换后（举例）：
```
- 10年UI设计老兵，设计总监，美院出身
```

---

## 第二步：配置项目信息（必做）

编辑 `douyin-project/references/project-config.md`：

1. **抖音账号信息**：填入你的账号名、抖音号、粉丝数、城市
2. **素材库路径**：填入你本地的素材库目录路径
3. **系统环境**：确认 Python/Node.js 路径正确

### 合集配置

将示例合集替换为你自己的合集：

```
| 【合集1】 | 【参与人数】 | 【内容方向】 |
| 【合集2】 | — | 【合集描述】 |
```

---

## 第三步：初始化状态文件（必做）

在你的项目根目录（运营模板包所在目录）创建 `.cheat-state.json`：

```json
{
  "schema_version": "1.1",
  "skill_version": "v5.20",
  "rubric_version": "v1.0",
  "content_form": "opinion-video",
  "typical_duration_seconds": 90,
  "target_publish_cadence_days": 2,
  "calibration_samples": 0,
  "consecutive_directional_errors": [],
  "shoots": [],
  "pending_retros": [],
  "pool_status": "none",
  "pool_path": "04_方案案例/",
  "data_layer": "markdown",
  "data_collection": "manual",
  "baseline_plays": null,
  "benchmark_status": "none"
}
```

**字段说明**：

| 字段 | 含义 | 建议值 |
|:-----|:-----|:------|
| `content_form` | 内容形态 | `opinion-video`（观点口播） |
| `typical_duration_seconds` | 标准时长 | 60-90 |
| `target_publish_cadence_days` | 发布间隔天数 | 2（隔日更） |
| `baseline_plays` | 播放量中位数 | 初始填 `null`，有3条数据后更新 |

---

## 第四步：填入历史数据（建议）

编辑 `douyin-script-scoring/references/historical-data.md`，将模板数据替换为你的实际视频数据：

```
| 【期数】 | **【播放量】** | 【完播率】 | 【收藏】 | 【分享】 | 【涨粉】 | 【类型】 | 【教训】 |
```

替换示例：
```
| 第1期 | **1.2万** | 8.5% | 45 | 12 | 86 | 情绪故事 | 开头铺垫太长 |
| 第2期 | **523** | 3.2% | 8 | 2 | 3 | 方法论 | 干货出现太晚 |
```

**建议**：至少填入3条历史数据，评分和预测才会更准确。

---

## 第五步：验证安装

在 WorkBuddy 对话中输入：

```
状态
```

如果看到状态看板输出，说明安装成功！

---

## 可选配置

### 自动化任务

在 WorkBuddy 中创建定时任务：

| 任务 | 频率 | 描述 |
|:-----|:-----|:-----|
| 自动复盘提醒 | 每日 10:00 | 检查是否有待复盘视频 |
| 数据修正提醒 | 每3天 | 提醒导出最新数据 |

### MemPalace 集成

如果你安装了 MemPalace skill，可以启用记忆宫殿同步，将复盘洞察自动写入长期记忆。
