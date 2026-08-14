---
name: case-report-ppt
description: 安全改造临床病例汇报、出科汇报和教学病例 PowerPoint（PPT/PPTX）。当需要换科室或病种、重构病例内容、保留既有模板视觉、优化病例汇报排版、用诊断证据链标红异常指标、设置克制动画/切换、或对医学逻辑和最终幻灯片进行质检时使用。
compatibility: opencode
metadata:
  format: agent-skills
  locale: zh-CN
---

# 病例汇报 PPT 改造

遵循“模板保真、内容重构、适度创新”。优先保护原文件和患者隐私；医学内容仅据已提供资料整理，不补造患者事实或替代临床判断。

## 约定常量（全篇唯一来源）

- 通用模板：`templates/病例汇报_通用模板.pptx`（本 skill 目录内的母版模板，相对本 SKILL.md 路径）。使用时用文件系统复制到目标 PPT 目录，不直接编辑母版。

## 开始

1. 先用 OpenCode 的文件读取能力加载 [workflow.md](references/workflow.md)，并在任何编辑前创建、验证安全副本。
2. 盘点源 PPT 的页面、母版、背景、版式、可编辑元素和已有动画；建立唯一的病例数据源。
3. 按任务读取需要的参考文件：

| 情形 | 必读文件 |
| --- | --- |
| 病例资料、诊断、检查、隐私或医学一致性 | [medical-content.md](references/medical-content.md) |
| 重排版、字体、缩进、动画、切换或可视化表达 | [layout-design.md](references/layout-design.md) |
| PowerPoint MCP、PowerShell COM、格式保留或兼容性问题 | [powerpoint-technical.md](references/powerpoint-technical.md) |
| 完成前审查、渲染检查、恢复与交付 | [validation.md](references/validation.md) |
| 页面改造取舍或文字示例 | [examples.md](references/examples.md) |

从项目根目录使用本技能时，参考文件位于 `.opencode/skills/case-report-ppt/references/`。不要假设 OpenCode 已安装 PowerPoint MCP；先检查当前可用工具。无 PowerPoint 自动化能力时，只整理内容、提出可执行修改清单或请求用户提供可编辑环境，不伪称已修改 PPT。

## 不可突破的边界

- 不改页面尺寸/比例、主题、主题色、核心品牌字体、主背景、Logo、母版核心元素、页眉页脚或页码体系，除非用户明确授权。
- 不随意删页、改页序、删流程页或整体替换母版。
- 不在原件上试错；只编辑已验证为当前激活文档的副本。
- 不编造病史、检查、治疗、疗效、指南结论或正常值；不确定项标注“待核实”。
- 删除或遮蔽可识别个人信息；不把病例材料上传至未经授权的外部服务。

## 默认决策

- 模板选择：用户指定了已有 PPT 时以该 PPT 为模板改造；未指定、或要求「根据模板生成」时，把 skill 内通用模板 `templates/病例汇报_通用模板.pptx` 复制到目标目录后作为起点（复制而非直接编辑母版）。
- `layout_change_level = 2`（适度重排）：保留视觉语言，按医学叙事重组信息。
- 呈现方式可创新：不要求全篇套用相同表格或列举，根据内容选择最合适的可视化形式，同时保持视觉语言统一。
- 仅用克制的 Fade、Appear、Wipe 或简单 Morph；动画服务讲解顺序，单页通常不超过 5 个动画元素。
- 诊断关键阳性信息和异常指标使用 `#EE0000`，并保留语义、单位、参考范围和采集时间。
- 每次明显改动后做页面级检查；完成后按 validation 清单逐页渲染核验。

## 交付

保存为明确命名的最终副本，保留原件和必要的恢复副本。汇报时说明：输出路径、修改范围、待临床核实项，以及是否通过最终质检。
