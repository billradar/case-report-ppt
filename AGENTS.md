# 病例汇报 PPT 改造（case-report-ppt）

安全改造临床病例汇报、出科汇报和教学病例 PowerPoint 的知识库。核心原则：**模板保真、内容重构、适度创新**。

本目录是一套跨 agent 的 skill：`SKILL.md` 为 Agent Skills 入口（Claude Code / opencode），本 `AGENTS.md` 为通用入口（Copilot / Cursor / Windsurf / Cline / Codex 等）。

## 核心知识位置

核心知识在 `references/` 中，按任务按需读取，不要一次全读：

| 情形 | 读取文件 |
| --- | --- |
| 安全工作流（保护原件、先复制后编辑、恢复） | `references/workflow.md` |
| 病例资料、诊断、检查、隐私、医学一致性 | `references/medical-content.md` |
| 布局、字体、缩进、动画、呈现方式 | `references/layout-design.md` |
| PowerPoint MCP / PowerShell COM 技术坑 | `references/powerpoint-technical.md` |
| 完成前审查、渲染检查、交付 | `references/validation.md` |
| 页面改造取舍与文字示例 | `references/examples.md` |
| 现成高质量病例、选病例 / 扩病例库 | `references/case-library.md` 与 `cases/` |

## 核心原则（摘要）

- **模板保真**：只改内容、不改模板；不改页面尺寸/主题/母版/页眉页脚/页码体系，除非用户明确授权
- **先复制、后编辑**：OneDrive/PowerPoint 的 AutoSave 会实时写回当前文档，任何编辑前必须先另存/复制副本
- **区分资料性质**：真实病例以提供的病历资料为唯一患者事实来源；病例库内容作为虚构教学病例。PPT 标题页或资料来源页明确标注“真实病例（已脱敏）”或“虚构教学病例”；缺失项标注“待核实”，不得随机设定结局
- **去标识化**：移除姓名、住院号、证件、联系方式等（含截图、页眉页脚、备注）
- **异常标红**：诊断关键阳性信息和异常指标用 `#EE0000`，保留单位、参考范围、时间
- **标题不重复**：同一章节标题全篇只出现一次
- **按需灵活**：页数、列表/表格/卡片行列数按需增减，不局限固定数量；呈现方式可创新

## 模板

- 通用母版模板：`templates/病例汇报_通用模板.pptx`（二进制，被 .gitignore 忽略，需本地保留）
- 模板选择：用户指定已有 PPT 时用它改；未指定/要求按模板生成时，复制 `templates/` 内母版到目标目录后使用，母版永不修改

## 工具依赖（重要）

- 先探测当前环境可用的 PPT 编辑、预览和重新打开验证能力，按 `references/powerpoint-technical.md` 选择工具。
- ppt-mcp 是适用环境下的可选路径；仅在用户选择该路径时按其项目文档安装和配置，不默认修改客户端设置。
- 无可靠编辑能力时只整理内容、建立病例数据源并给出可执行修改清单，**不伪称已修改 PPT**

## 完成标准

交付时说明：输出路径、修改范围、待临床核实项、是否通过质检；保留原件，交付后删除工作副本。
