# 文本与铅笔分镜规范

## 第 6 步：文本分镜文档（默认）+ 铅笔分镜（可选）

当第 5.5 步自检通过后，在产出任何分镜素材前，先给出分镜模式选择卡：

- **仅文本分镜文档（默认推荐）** — 以一个画布文本节点承载全部镜头分镜，按章节方式组织。结构参考半叙事戏剧分镜：每镜字段（标题 / Hook / 场景 / 角色 / 空间锚点 / 连续性 / 表演）+ 皮克斯式每面板四象限内容 + 可选 ASCII 排版。低成本但可承载完整质检信息。第 7 步视频模型会直接以此作为逐镜渲染依据。
- **文本分镜文档 + 多面板铅笔图（可视化模式，可选）** — 文本分镜文档仍作为权威产物，同时每镜再生成一张多面板铅笔图用于人工复核。成本更高，适用于用户在生成视频前希望先看视觉预览，或在挤压-弹性姿态/轮廓是主要风险点并希望先目视核对时。

将已选分镜模式写入项目简报，并在第 7 步、第 9 步及重生成纪律中沿用。

### 默认路径：单一文本分镜文档

生成一个名为 `<title> text storyboards` 的画布文本节点（整个短片一个文档）。该文档在第 7 步仍是渲染权威参考，即使你同时产出铅笔图。文档结构需反映半叙事戏剧分镜，每个镜头一段，方便用户跨镜头阅读连续性，无需跳节点。

文档头部信息（文档顶部）：

- 项目标题、已确认视频模型、已确认分辨率、分镜模式、自检状态（例如 `shot-table self-check: passed at <timestamp>`）
- 简短目录：列出每个镜头的 Hook 与锚点（`S01`、`S02`…）和 section anchor，便于跳转

每个镜头段落结构（每个镜头一个 `##` 标题，按镜头顺序），字段按顺序全部必须包含；这是对半叙事戏剧分镜的直接适配：

1. **镜头标题与时长** — 简洁的人类可读标题 + `S<N> / <duration>s`（如 `S03 / 6s`）
2. **Hook 类型** — 受控词库中的一个值：`setup` / `visual-joke` / `reversal` / `reveal` / `callback` / `suspense` / `tender` / `chase` / `expression-beat` / `climax`，用于每集 Hook 分布自检。
3. **场景与角色** — 精确场景卡名与当前在屏角色名（绑定角色卡）。
4. **空间锚点卡**（必填，四个子字段；与半叙事戏剧分镜直接对齐）：
   - `固定地标` — 命名地标及其屏幕相对位置（如 `door-frame: right third`、`kitchen-island: center bottom`）
   - `角色位置（摄像机视角）` — 每个在屏角色的相对位置、朝向、初始姿态
   - `离场角色状态` — 上一镜有但本镜无的角色及其离屏位置和原因
   - `光照基线` — 继承场景卡主/补/轮廓光方向，并加镜头级修正
5. **连续性**（对应半叙事戏剧 handoff 字段）：
   - `从 S(N-1) 的连续性` — 一到两句引用上一镜末尾状态
   - `到 S(N+1) 的连续性` — 一句设定下镜开场
6. **双重绑定** — `[char:角色名-01] [char:角色名-02] ... [scene:场景名] [hook: visual-joke]`，使用精确角色卡名、场景名和 Hook 类型。这些为分镜专用标记，视频模型在渲染时剥离。
7. **每面板四象限内容**（按时间顺序每面板一组；即皮克斯式每秒指令，保留自表格行）：
   - `Timecode` — 如 `0–1s`
   - `姿态 + 表情` — 具体身体姿态、轮廓、关键道具握法、视线走向、表情路径；弹性动作要明确写出 squash/stretch、anticipation、overshoot。该字段通常最大，也正是模型读取的视觉节拍主干。
   - `Camera` — 景别、镜头运动（push / pull / pan / tilt / handheld-shake / locked / orbit），如适用写入 Dutch-angle 说明
   - `Audio + Anchor` — 音频提示（`♪ narration: ...` / `dialogue: ...` / `SFX: ...` / `silent`）以及空间锚点备注（如 `door-frame: right third` / `Mia: center midground facing camera`）
   - 表演备注（对应半叙事戏剧）：旁白秒标注 `narrator-mouth-closed: true`；画内对白标注 `mouth-open: speaker` 并写清表情路径、视线方向、身体动作变化
8. **布局规则**（每镜适用）：
   - 3 秒镜头 → 3 格（每秒一格）
   - 4 秒镜头 → 4 格
   - 5 秒镜头 → 5 格
   - 6 秒镜头 → 6 格
   - 7 秒以上 → 每秒一格，关键子秒节拍（如 `2.0–2.5s`）仅在该拍是该镜关键 Hook 时新增
   - 面板覆盖从首帧到末帧无时间空档
9. **分面板绑定**：
   - 绑定表格行中精确角色卡，锁定外观、脸部、发型、体型比例、服装、关键道具和身份标识；角色名使用与表格一致。
   - 绑定行中精确场景卡，保留环境、道具、地标、运动路径和空间逻辑。
10. **可选 ASCII 区块（强烈建议）**：
    - 每面板可加小型 ASCII 草图（或整镜一张总草图），便于用户秒级扫描空间布局，无需渲染图。
    - 示例：
      ```
      [0-1s]  Mia (L, mid)         door-frame (R)
              ──kneels, hands on apple basket──
              cam: low push-in, locked
              audio: silent | anchor: basket center-bottom
      [1-2s]  ...
      ```
    - ASCII 仅作辅助信息；视频模型读的是 `Per-panel four-quadrant content` 结构化内容，而非 ASCII。
11. **分镜专属标记**：
    - 关键拍可在时间码后加 `[BEAT]`
    - 若面板需显式交接状态到下一个面板或下一镜，追加 `[HANDOFF → ...]`，如 `[HANDOFF → S04 opening]`

每镜段落模板（可直接复制）：

```markdown
## S03 / 6s — Title: 奶奶把苹果筐递给 Mia

- **Hook type**: reveal
- **Scene & characters**: scene:kitchen | char:Mia, char:Grandma
- **Spatial anchor card**:
  - Fixed landmarks: door-frame (right third), kitchen-island (center bottom)
  - Character positions: Mia (L, midground, facing camera) | Grandma (R, foreground, facing Mia)
  - Exited character status: —
  - Lighting baseline: warm overhead key + cool bounce right
- **Continuity from S02**: 奶奶弯下腰从中岛拿起苹果筐
- **Continuity to S04**: Mia 接住筐转身，门铃响起
- **Double-binding**: [char:Mia] [char:Grandma] [scene:kitchen] [hook:reveal]

### Per-panel four-quadrant content

#### 0–1s
- Pose + Expression: 奶奶弯腰双手持筐；Mia 左侧站姿，眼神好奇
- Camera: locked medium shot, eye-level
- Audio + Anchor: silent | Mia: L midground | basket: center bottom
- Performance: [BEAT]

#### 1–2s
- Pose + Expression: 奶奶手臂伸向 Mia，筐倾斜；Mia 双手前伸准备接
- Camera: locked medium shot, eye-level
- Audio + Anchor: ♪ SFX: basket rustle | anchor: door-frame: right third
- Performance: [HANDOFF → S04 opening]

#### 2–3s
...

### ASCII layout (optional)
[0-1s]  Grandma (R, fg)        door-frame (R, bg)
        ──lifts basket──        Mia (L, mid)
        cam: locked | silent
[1-2s]  ...
```

所有章节写完后，放到画布并直接进入第 7 步；默认模式不调用任何图像生成模型。

### 镜头级提取（高迭代模式）

默认单文档有利于全局阅读与连续性核对。若用户在第 6 步后标记某镜头重迭代（常见于高潮/追逐/滑稽拍 where 该镜头每面板需多轮修订），可将该段落提取到独立文本节点：

- 用户信号：第 6 步后出现如“我先看 S05”“S05 需要重做”“extract S05”或在分镜审批选择卡中选中某镜。
- 提取机制：
  1. 新建画布文本节点 `<title> S05 text storyboard (extracted)`。
  2. 将原文档 `## S05` 全段内容移入该节点。
  3. 在原文档中用一行占位替换：`> S05 — extracted to standalone node (see `<title> S05 text storyboard (extracted)`)`。
  4. 第 7 步读取该镜头时使用独立节点，其它镜头仍从主文档读取。
- 回填：用户满意后，将独立节点最新版内容回插到占位处，并归档独立节点。
- 多镜提取时，每镜独立节点；主文档用占位维护清单。

提取机制为高压力镜头提供局部迭代能力，避免默认拆分；仅在需要时启用。

### 可选路径：多面板铅笔分镜（可视化模式）

若用户在分镜模式选择卡中选了可视化模式，在文本分镜文档之外，额外为每行镜头生成一张多面板铅笔分镜图。文本文档仍是渲染权威，铅笔图仅作人工复核，不是最终成片画质结果。

每张铅笔分镜图要求：

- **双重绑定标签（右上角，必填）**：
  - `[char:角色名-01] [char:角色名-02] ...` — 行内精确角色名
  - `[scene:场景名]` — 精确场景名
  - `[shot: S03] [dur: 6s] [hook: visual-joke]` — 镜头号、时长、Hook
  - 这些标签为分镜专用标记，视频渲染会剥离。
- 绑定表格行中的角色卡，锁定外观、脸、发型、体型比例、服装、签名道具和身份。
- 绑定表格行中的场景卡，保留环境、道具、地标、运动路径、空间逻辑。
- 将该行每秒指令转为一个面板或关键 beat 面板；4 秒镜头通常产 4 面板，6 秒镜头通常 6 面板；子秒关键beat仅在必须时新增。
- **面板物理布局（必填）**：
  - 3 秒镜头 → 1×3 条带
  - 4 秒镜头 → 2×2 网格
  - 5 秒镜头 → 上排 3 + 下排 2
  - 6 秒镜头 → 2×3 网格
  - 7 秒以上 → 3 行均衡面板
  - 每个面板占相同画布面积，不得让某一面板过大压住其它
- **面板四象限内容（必填）**：
  - 左上：时间码（如 `0–1s`）
  - 右上：姿态+表情草图（最大区域，核心视觉）
  - 左下：镜头图标+运动箭头（push/pull/pan/orbit/locked）与简短 Dutch-angle 注记
  - 右下：音频提示（如 `♪ narration: "I knew it."` / `SFX: door creak` / `silent`）与锚点标注（如 `door-frame: right third`）
- 同一张图按时间顺序排列面板，不要把不同镜头合到一张图里。
- 每面板要标注时间码，且对应显示 pose、表情、动作、镜头运动、道具位置、SFX 和连续性交接。
- 仅输出黑白铅笔线稿：无颜色、无成片打光、无精修 3D 渲染。
- 允许在镜头上标注 shot number，并按需添加镜头运动图标/标记。
- 可加入分镜专用标注：铅笔结构线、动作箭头、镜头路径图标、节奏标记、小注释。
- 仅作为渲染参考素材，不作为最终成片成品。

### 分镜审批（两种模式）

当文本分镜段落和（若开启）铅笔图全部产出后，按顺序放入画布并分组：
- `<title> text storyboards`（默认模式，单文档）
- `<title> text storyboards + multi-panel pencil storyboards`（可视化模式，文本文档与铅笔图分组，因铅笔图含双重绑定标签、ASCII 与镜头编号，文本节点不应混合）

展示用户选择卡：

- 通过分镜并开始镜头渲染（推荐）
- 提取/回填镜头（将段落在文档与独立节点间移动）
- 重画选中铅笔分镜（可视化模式）
- 修正角色一致性
- 修正场景逻辑
- 修正镜头标记
- 修正音频/锚点标记

### 分镜生成失败兜底（仅可视化模式）

若铅笔分镜无法满足质量（如布局塌缩、标签不可读、面板合并、角色不一致），在向用户确认前按以下顺序处理：

1. **第一次重试**：用更紧的提示重生成该镜头分镜，明确要求四象限布局、`[char:…] [scene:…] [shot:…]` 标签和每面板内容规则。
2. **第二次重试**：去掉右下角音频/锚点文字（保留一个小 `♪` 的空格）以降低文本负荷，通常能修复标签可读性问题。
3. **第三次重试**：减少面板数（例如 6 面板 → 5 面板，将动作最弱的两秒合并）并将摄像机图标简化为单箭头。
4. **同一镜头连续三次失败后**：暂停并给用户选择卡：
   - 仅该失败镜头切换为块色分镜（姿态灰框，不要铅笔线）
   - 该镜头取消铅笔图，转而仅依赖文本分镜文档
   - 将该镜头在第 5 步拆为两个更短镜头后重跑 5.5
   - 人工提交参考图绑定

默认文本模式下无需整套兜底：文本分镜仅在模型无法产生连贯结构化文本时失败，此时回到第 5 步修镜头表即可。
