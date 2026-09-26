# 病例汇报 PPT 改造（case-report-ppt）

安全改造临床病例汇报、出科汇报和教学病例 PowerPoint 的跨 agent skill。核心原则：**模板保真、内容重构、适度创新**。

## 功能

- 换科室 / 换病种 / 换指导老师，**只改内容、不改模板**
- 支持操作者自行提供详细病例资料（以其为唯一事实来源），或仅凭科室/病种生成去标识化教学病例
- 保留原模板的背景、母版、配色、页眉页脚、页码、页面顺序
- 诊断证据链 + 异常指标标红（`#EE0000`）
- 排版优化：字号规范、首行缩进、修复孤行、标题不重复、呈现方式多样化
- 克制动画 / 切换（Fade、Appear、Wipe、Morph）
- 医学一致性检查 + 去标识化
- 完成后逐页质检清单（内容 / 视觉 / 技术）
- 内置病例库（`cases/`，20 科室 120 例教学病例及 8 例死亡病例讨论）

## 病例库（预置）

`cases/<科室>/` 内置 20 个科室、每科室 5 个常见病种与 1 个疑难病种，共 120 例；`cases/死亡病例讨论/` 另有 8 例，连同 `cases/_TEMPLATE.md` 共 129 个 Markdown 文件。全部按**虚构教学病例**处理，不能冒充真实病历。

按科室/病种选用；不足时据 `cases/_TEMPLATE.md` 扩展。索引与选用规则见 [references/case-library.md](references/case-library.md)。

## 目录结构

```
case-report-ppt/
├── SKILL.md                      # Agent Skills 入口（Claude Code / opencode）
├── AGENTS.md                     # 通用入口（Copilot / Cursor / Windsurf / Cline 等）
├── README.md
├── .gitignore                    # templates/ 已忽略
├── templates/
│   └── 病例汇报_通用模板.pptx     # 母版模板（二进制，不入库）
└── references/
    ├── workflow.md               # 安全工作流
    ├── medical-content.md        # 病例内容与医学一致性
    ├── layout-design.md          # 布局、字体与演示设计
    ├── powerpoint-technical.md   # PowerPoint MCP / COM 注意事项
    ├── validation.md             # 最终质检与交付
    ├── examples.md               # 具体改造示例
    └── case-library.md           # 病例库索引与选用规则
cases/
  ├── _TEMPLATE.md                # 新增病例模板
  ├── <科室>/                     # 20 科室，每科 6 例
  │   └── <序号>-<病种>.md
  └── 死亡病例讨论/               # 8 例
```

## 兼容的 agent

- **Claude Code / opencode**：直接作为 Skill 加载（`SKILL.md`，agent-skills 格式）
- **GitHub Copilot / Cursor / Windsurf / Cline / Codex 等**：自动读取 `AGENTS.md` 通用入口

> 说明：核心知识在 `references/`（纯 Markdown，各 agent 通用）；实际修改 PPT 需要 PowerPoint MCP，无 MCP 的 agent 只能整理内容、给出可执行修改清单。

## 使用前提

- 支持以上任意一种 agent
- 可用的 PPT 编辑工具，以及逐页预览和重新打开验证能力；ppt-mcp 是可选路径之一
- 使用 ppt-mcp 时，环境还需满足该工具的运行要求

## 快速开始

在 opencode 中直接说明需求即可触发，例如：

- 「把儿科病例汇报改成感染科，病种选发热伴血小板减少综合征」
- 「根据模板生成一份出科汇报」
- 「按这份病例做一份出科汇报：<粘贴详细病史/查体/检验/诊断/治疗资料>」

**模板选择规则**：用户指定了已有 PPT 时，以该 PPT 为模板改造；未指定、或要求「根据模板生成」时，从 `templates/病例汇报_通用模板.pptx` 复制到目标目录后使用。

## 工作流概览

1. **接收与边界确认**：确认源文件、命名、调整范围，确定模板来源
2. **保护原件**：先复制、后编辑（OneDrive AutoSave 会实时写回，务必先另存/复制）
3. **基线盘点**：记录页面、母版、版式、可编辑元素与已有动画
4. **统一病例数据源**：先统一数值/日期/单位/诊断，再写入页面
5. **内容 / 布局 / 顺序**：替换内容 + 标红 + 排版（页数/行列数按需增减）
6. **渐进保存与恢复**：按章节保存，失败回退到恢复点
7. **最终化**：按 validation 清单逐页质检，交付最终副本

## 命名约定

- 工作副本：`NAME-科室-病例汇报_working.pptx`
- 最终版：`NAME-科室-病例汇报.pptx`
- 不要用笼统的 `test.pptx`

## 注意事项

- **模板文件不入库**：`templates/病例汇报_通用模板.pptx` 已被 `.gitignore` 忽略，clone / 分享项目后需手动放入（或从本地原文件复制）
- **病例性质须明示**：PPT 标题页或资料来源页标注“虚构教学病例”或“真实病例（已脱敏）”；前者的数值、处置和结局须经临床人员审核，不得随机设定死亡结局
- **去标识化**：移除姓名、住院号、证件、联系方式等可识别信息（含截图、页眉页脚、备注）
- **母版永不修改**：编辑前先复制模板到目标目录，母版保持干净

## 许可

本项目为个人使用的 skill，医学内容仅用于教学呈现。
