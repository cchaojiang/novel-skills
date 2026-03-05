# Novel Planner Skill

小说卷大纲生成专用，用于根据世界观设定创建卷级剧情大纲。

---

## 适用场景

- 根据世界观设定生成卷级剧情
- 不需要设计世界观（由 world-builder 负责）
- 支持500-700章

---

## 输入（来自 story-designer + world-builder）

### 必须加载的文件

| 文件 | 说明 | 来源 |
|------|------|------|
| `story_outline.md` | 故事主线（10卷剧情架构） | story-designer 输出 |
| `world_setting.md` | 完整世界观设定 | world-builder 输出 |
| `character_setting.md` | 人物设定 | world-builder 输出 |
| `realm_system.md` | 境界体系 | world-builder 输出 |
| `cultivation_system.md` | 修炼体系 | world-builder 输出 |
| `factions.md` | 势力格局 | world-builder 输出 |
| `faction_relations.md` | 势力关系 | world-builder 输出 |
| `dungeons.md` | 秘境遗迹 | world-builder 输出 |
| `protagonist_faction.md` | 主角势力演变 | world-builder 输出 |

### 可选输入
- 卷数（默认10）
- 章节数（默认665）

---

## ⚠️ 核心质量要求

### 1. 只生成卷级内容
- ❌ 不要生成章节详情（如：第1章，第2章...）
- ✅ 只生成每卷的整体剧情描述

### 2. 每一卷质量必须一致
- 每一卷的核心剧情描述需要**500字以上**
- 每一卷的爽点需要**3-5个**
- 每一卷的伏笔需要**2-3个**
- 不能"前几卷写得好，后面几卷敷衍"

### 3. 每卷必须包含的内容

```markdown
# 第X卷：卷名

## 基本信息
- 卷名：
- 副标题：
- 章节范围：
- 主题：
- 地点：
- 目标境界：

## 核心剧情（详细描述，500字以上）
本卷的核心故事情节，需要详细展开

## 主要人物
- 主角：
- 主要配角：
- 反派：

## 本卷爽点（3-5个）
1. xxx
2. xxx

## 本卷伏笔（2-3个）
1. xxx（埋入点）
2. xxx

## 本卷结局
本卷结尾的剧情走向

## 承上启下
- 承接上一卷：
- 引出下一卷：
```

---

## 一、三个Skill协同工作

```
world-builder（构建宏观世界）
├── 输入：用户参数（标题/题材/主角/修炼体系）
├── 输出：world_setting.md + character_setting.md
└── 职责：境界/修炼/势力/地图/冲突/人物
        ↓
story-designer（全本主线故事设计）
├── 输入：world_setting + character_setting + 用户参数
├── 输出：story_outline.md
└── 职责：800章主线/16-20卷/伏笔体系
        ↓
novel-planner（生成详细卷大纲）
├── 输入：story_outline + world_setting + character_setting
├── 输出：volume_outline.md + foreshadow_table.md
└── 职责：卷级剧情/伏笔追踪
```

---

## 二、项目结构

```
/home/ubuntu/.openclaw/workspace/novel/
├── data/novel/
│   ├── novel_title.txt        # 小说标题
│   ├── world_setting.md       # 世界观设定（来自world-builder）
│   ├── character_setting.md  # 人物设定（来自world-builder）
│   ├── volume_outline.md    # 卷大纲
│   └── foreshadow_table.md  # 伏笔追踪表
```

---

## 三、Agent（2个）

| Agent | 负责模块 |
|-------|---------|
| **GlobalPlanner** | 卷设计/伏笔/冲突 |
| **VolumePlanner** | 卷结构划分 |
| **OutlineReviewer** | 校验卷大纲质量 |

> 注意：章节详细生成由独立的 `chapter-planner` Skill 负责

---

## 四、工作流（15步）

```
Step 1: load_inputs         加载世界观/人物设定
Step 2: design_volume_structure  划分卷次
Step 3: design_volume_1    设计第1卷
Step 4: design_volume_2    设计第2卷
...（继续到所有卷）
Step N: design_volume_12   设计第12卷
Step N+1: generate_foreshadow_table  伏笔追踪表
Step N+2: review_volumes   校验所有卷
Step N+3: final_audit     最终审核
Step N+4: save_volume_outline  保存卷大纲
```

---

## 五、质量保证原则

1. **每一卷都要详细完整**
   - 核心剧情：500字以上
   - 爽点：3-5个
   - 伏笔：2-3个
   - 主要人物：明确

2. **保持质量一致**
   - 第1卷用心写，后续卷同样用心
   - 不能"开头精彩，后面敷衍"
   - 每卷都要有高潮点

3. **伏笔贯穿全文**
   - 前期卷埋入伏笔
   - 后期卷呼应伏笔
   - 形成完整闭环

---

## 六、输出文件

```
./data/novel/volume_outline.md    - 12卷详细大纲
./data/novel/foreshadow_table.md - 伏笔追踪表
```

---

## 七、工作流协同

```
用户输入参数
        ↓
world-builder（构建世界）
        ↓
world_setting.md + character_setting.md
        ↓
novel-planner（生成卷大纲）
        ↓
volume_outline.md + foreshadow_table.md
        ↓
chapter-planner（生成章节）
        ↓
volume_01_chapters.md（每卷章节）
```
