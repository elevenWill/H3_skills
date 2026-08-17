---
name: h3-prompt-writing
description: 为 T2VA、I2VA、FL2VA、L2VA 和 Ref2VA 编写 MiniMax H3 视频生成提示词。适用于将多模态请求改写为 H3 提示词结构，编写 integrated_multimodal_description、overall_soundscape 和 non_diegetic_music，匹配关键帧，或为图像、视频和音频定义参考标签。
---

# H3 Prompt Writing

## Workflow

1. 识别输入模式：T2VA、I2VA、FL2VA、L2VA 或完整参考模式 Ref2VA。
2. 对于基础文本/关键帧模式，读取 `references/base-en.txt`，并遵循其中的最终提示词结构。
3. 对于完整参考模式，读取 `references/ref-en.txt`，并遵循其中的六部分改写格式。
4. 保持所选指南中的字段名、部分顺序、标签和时间标记法完全一致。

## Base Modes

- T2VA：根据文本构建完整的视听时间线。
- I2VA：从第一帧开始，并从该帧向前展开。
- FL2VA：描述第一帧与最后一帧之间的连续路径。
- L2VA：推断合理的开场，并逐步收束到所提供的最后一帧。

按照 `references/base-en.txt` 中展示的顺序使用 `integrated_multimodal_description`、`overall_soundscape` 和 `non_diegetic_music`。

## Full-Reference Mode

Ref2VA 改写应依次使用 `subject_definitions`、`summary`、`retention_analysis`、`detailed_description`、`overall_soundscape` 和 `non_diegetic_music`。参考标签必须在所有部分中保持一致。

读取 `references/ref-en.txt`，了解标签规则、保留分析以及完整示例。

## Output Rules

- 改写部分使用英文；对话、歌词和画面中可见的场景文字保留其原始语言。
- 描述每个镜头时，应说明构图、主体、环境、动作、摄影机、声音，以及被参考内容出现的准确时间点。
- 避免剧情摘要、未解决的参考标签，以及与请求时长不匹配的时间安排。
