# Chapter Writer Skill

根据章节大纲生成每个章节的正文内容，包含完整的创作、校验、润色流程。

---

## 适用场景

- 根据章节大纲生成章节正文
- 每章正文3000-4000字
- 包含4层校验 + 润色

---

## 输入（来自 chapter-planner + world-builder）

| 参数 | 来源 |
|------|------|
| `volume_N_chapters.md` | chapter-planner 输出的章节大纲文件 |
| `target_chapter` | 要生成的章节号（如：第1章） |
| `world_setting.md` | world-builder 输出的世界观设定 |
| `character_setting.md` | world-builder 输出的人物设定 |
| `foreshadow_table.md` | 伏笔追踪表 |
| `prev_chapter_content` | 上一章正文（用于衔接） |

### 输入处理

1. **读取章节大纲文件**：`volume_N_chapters.md`
2. **提取目标章节**：从大纲中找到对应章节的设计
3. **加载世界观设定**：从 world_setting.md 获取境界体系等信息
4. **加载人物设定**：从 character_setting.md 获取人物性格
5. **加载上一章正文**：用于开头衔接

---

## 每章大纲包含的信息

```markdown
### 第1章 章节标题

- **字数**: 3000-3500
- **人物**: xxx
- **地点**: xxx
- **情节**:
  - 起：xxx
  - 承：xxx
  - 转：xxx
  - 合：xxx
- **目标**: xxx
- **爽点**: xxx
- **伏笔**: xxx
- **衔接**: 承接上一章xxx
- **钩子**: xxx
```

---

## Agent（5个）

| # | Agent | 职责 |
|---|-------|------|
| 1 | **NovelWriter** | 撰写初稿 + 重写 |
| 2 | **NovelReviewer** | 综合审核（字数/逻辑/OOC） |
| 3 | **WorldKeeper** | 世界观校验（境界/势力/功法） |
| 4 | **CharacterKeeper** | 人物校验（性格/OOC） |
| 5 | **NovelPolisher** | 润色 + 文风统一 |

> 注：NovelPlanner 在 chapter-planner 阶段已完成章节大纲设计

---

## 工作流（9步）

### 阶段1：准备（读取所有输入）
```
Step 1: read_outline_file     读取章节大纲文件（volume_N_chapters.md）
Step 2: extract_chapter_design 提取目标章节的10项设计
Step 3: load_world_setting   加载世界观设定（world_setting.md）
Step 4: load_char_setting   加载人物设定（character_setting.md）
Step 5: load_foreshadow    加载伏笔追踪表
Step 6: load_prev_chapter  加载上一章正文（用于衔接）
```

### 阶段2：创作
```
Step 7: generate_draft      NovelWriter生成初稿（≥3000字）
```

### 阶段3：校验（4层）
```
Step 8: review_draft        NovelReviewer综合审核
        ↓ 不通过 → 重写
        
Step 9: world_check         WorldKeeper世界观校验
        ↓ 不符合 → 重写
        
Step 10: char_check         CharacterKeeper人物校验
        ↓ OOC → 重写
```

### 阶段4：润色
```
Step 11: polish             NovelPolisher润色 + 文风统一
```

### 阶段5：发布
```
Step 12: save_chapter       保存本地（chapter_001.md）
Step 13: upload_feishu     上传到飞书
```

---

## 校验流程图

```
初稿 → 综合审核(4) → 世界观(5) → 人物(6)
  │         │          │          │
  │         └──────────┴──────────┘
  │                        ↓
  └──────────────────→ 重写(回到Step3)
```

---

## 章节正文格式要求

```markdown
# 第1章 章节标题

[正文内容，3000-4000字]

章节开头：
- 承接上一章结尾
- 场景切入自然

章节发展：
- 情节推进
- 人物互动
- 冲突展现

章节高潮：
- 核心冲突爆发
- 爽点体现

章节结尾：
- 悬念钩子
- 为下一章铺垫
```

---

## 输出

```
./data/novel/chapter_{N}.md
例如：chapter_001.md
```

---

## 注意事项

1. **遵循大纲**：严格按照章节大纲的情节设计
2. **字数控制**：每章3000-4000字
3. **衔接自然**：开头承接上一章，结尾钩子引出下一章
4. **爽点体现**：突出大纲中的爽点情节
5. **伏笔埋入**：按伏笔ID埋入相应内容

---

## 核心约束（来自 novel-multiagent）

**允许的操作：**
- ✅ 将大纲描述扩展为具体情节
- ✅ 细化场景描写、对话、心理活动
- ✅ 添加过渡衔接
- ✅ 符合世界观的自然推理

**禁止的操作：**
- ❌ 添加大纲中没有的新人物
- ❌ 添加大纲中没有的新设定
- ❌ 添加大纲中没有的新剧情线
- ❌ 提前解锁能力或势力
