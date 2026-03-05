# Novel Skills

小说生成相关OpenClaw Skills，包含6个技能：

| Skill | 职责 |
|-------|------|
| **world-builder** | 构建世界观（境界/修炼/势力/地图/人物） |
| **story-designer** | 设计故事主线（10卷剧情架构） |
| **novel-planner** | 生成卷大纲（每卷500字以上剧情） |
| **chapter-planner** | 生成章节大纲（每章10项信息） |
| **chapter-optimizer** | 优化章节大纲（情节丰富、爽点增强） |
| **chapter-writer** | 撰写章节正文（3000-4000字/章） |

---

## 工作流

```
world-builder → world_setting.md
    ↓
story-designer → story_outline.md
    ↓
novel-planner → volume_outline.md + foreshadow_table.md
    ↓
chapter-planner → volume_N_chapters.md
    ↓
chapter-optimizer → volume_N_chapters_optimized.md
    ↓
chapter-writer → 章节正文
```

---

## 各Skill输入输出

| Skill | 输入 | 输出 |
|-------|------|------|
| world-builder | 用户参数 | world_setting.md |
| story-designer | world_setting.md | story_outline.md |
| novel-planner | world_setting.md + story_outline.md | volume_outline.md + foreshadow_table.md |
| chapter-planner | world_setting.md + volume_outline.md + foreshadow_table.md | volume_N_chapters.md |
| chapter-optimizer | world_setting.md + volume_N_chapters.md | volume_N_chapters_optimized.md |
| chapter-writer | world_setting.md + volume_N_chapters_optimized.md + foreshadow_table.md + 上一章正文 | 章节正文 |

---

## 输入文件说明

| 文件 | 说明 |
|------|------|
| world_setting.md | 世界观设定（境界/修炼/势力/地图） |
| story_outline.md | 故事主线（10卷剧情架构） |
| volume_outline.md | 卷大纲（每卷500字以上） |
| foreshadow_table.md | 伏笔追踪表 |
| volume_N_chapters.md | 章节大纲（每章10项信息） |
| volume_N_chapters_optimized.md | 优化后的章节大纲 |

---

## 使用方法

这些Skills需要配合OpenClaw使用，详细说明请参考各Skill目录下的SKILL.md文件。
