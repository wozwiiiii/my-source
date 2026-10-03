# 校招求职 Skill 合集

5 个从真实求职工作流中精简提炼的 AI Skill，覆盖「经历提炼 → 简历优化 → 简历持续维护 → 笔试备考 → 面试备考」全链路。适用于 WorkBuddy、Claude Code 等支持 SKILL.md 加载的 AI 助手环境，也可将 SKILL.md 全文作为系统提示词直接使用。

## 需求路由表：我该用哪个？

| 你的需求 | 使用 Skill | 触发示例 |
|---|---|---|
| 把做过的零散经历整理成简历可用素材 | `经历梳理` | "帮我梳理这段实习经历" |
| 改写已有简历，去掉过度包装与 AI 味 | `campus-resume-optimizer` | "优化我的简历" |
| 定期审核多版本简历 + 用代码核实数据 | `resume-continuous-optimizer` | "审核我的简历，核实里面的数字" |
| 生成校招笔试题（书面作答） | `campus-written-test-generator` | "生成今日笔试题" |
| 生成面试题（评分要点 + 连环追问） | `campus-ai-interview-builder` | "按我的项目出面试题" |

**简历类三者的分工**：`经历梳理` 从零提炼素材（口述 → 简历表述，缺数据用「XX」占位绝不编造）；`campus-resume-optimizer` 单次改写已有简历（STAR 重构 + 五项交叉审核）；`resume-continuous-optimizer` 周期性维护（多版本审核 + 代码事实核实 + 同步更新）。

**题库类两者的分工**：笔试考「会不会」（每岗 3 题：概念原理 / 代码实操 / 场景分析，书面作答）；面试考「说不说得清为什么」（每岗 4 题：技术基础 / 项目深挖 / 场景 / 手撕，独有【评分要点】+【追问方向】）。

## 各 Skill 简介

### 经历梳理
把口述的零散经历加工成「动作 + 内容 + 结果」句式的简历表述，按经历类型匹配量化维度，标注体现的能力。核心机制：缺口标注——没提供的数据用「XX」占位并汇总待补充清单，绝不编造。

### campus-resume-optimizer
校招简历单次优化器。角色定位「可信度审核员 + 结构化改写员」而非美化师：四步法（事实核查 → STAR 重构 → JD 匹配 → 五项交叉审核）。默认不自动触发（简历属敏感材料，需用户主动发起）。

### resume-continuous-optimizer
简历持续维护工作流：多版本简历定期审核、项目经历四层级结构化拆解（简介/背景/核心工作/产出）、代码事实核实（逐条验证简历数字）、多版本同步更新。安全设计：核实后先汇报、用户确认才修改；定时任务只出报告不自动改文档。简历来源不限（粘贴文本 / 本地文件 / 在线文档）。

### campus-written-test-generator
校招笔试题生成器，固定四岗位（AI 应用开发 / Agent 开发 / 技术支持 / 产品）× 每岗 3 题。核心资产是固化下来的四岗位考点库（原理 / 工程 / 业务三层），防止凭记忆命题导致质量漂移。技术支持按 TSE / 售前 / 售后细分差异化命题。所有参数可选、缺资料自动走通用考点，适合每日定时任务。

### campus-ai-interview-builder
校招面试题生成器，模拟面试官视角出题。有项目时题目强制锚定真实模块（标注【项目锚点】，只引用可核实信息）；无项目时第 2 题自动降级为通用项目场景题。生成后做 16 题考点交叉检查，防止四岗位重复考察同一考点。

## 安装

### WorkBuddy
- **用户级**（所有项目可用）：将 skill 目录复制到 `~/.workbuddy/skills/`
- **项目级**（仅当前项目）：复制到项目根目录 `.workbuddy/skills/`

### 其他 AI 助手 / 通用 LLM
将对应 skill 的 `SKILL.md` 全文作为系统提示词加载；含 `references/` 的 skill（两个题库生成器）需将引用文件一并附上。

## 工具依赖

| Skill | 需要的工具 | 说明 |
|---|---|---|
| 经历梳理 | 无 | 纯对话式加工 |
| campus-resume-optimizer | Read | 纯文本改写；默认仅手动触发 |
| resume-continuous-optimizer | Read / Write / Grep / Glob / WebFetch | 读简历与代码、核实后更新 |
| campus-written-test-generator | Read / Write / Grep / Glob | 读取项目资料、指定路径落盘 |
| campus-ai-interview-builder | Read / Write / Grep / Glob / WebFetch | 额外支持通过 URL 读取项目 README |

## 设计原则

- **真实性第一**：简历类 skill 禁止编造数据，缺失数字用「XX」占位或【请补充】提示，绝不虚构
- **防幻觉红线**：题库类 skill 引用项目细节必须可定位来源，编造细节列为头号禁区
- **缺参不反问**：题库类 skill 所有参数可选，缺省自动降级，适合接入定时自动化
- **修改先确认**：涉及文档修改的 skill 一律先汇报审核结果，用户确认后才执行
- **客观无褒贬**：命题与解析不对任何公司、技术、产品做主观褒贬

## 目录结构

```
my_skill/
├── README.md                          # 本文件
├── LICENSE                            # MIT
├── 经历梳理/
│   └── SKILL.md
├── campus-resume-optimizer/
│   └── SKILL.md
├── resume-continuous-optimizer/
│   ├── SKILL.md
│   └── README.md
├── campus-written-test-generator/
│   ├── SKILL.md
│   └── references/
│       ├── 考点库.md
│       └── 输出示例.md
└── campus-ai-interview-builder/
    ├── SKILL.md
    └── references/
        ├── 考点库.md
        └── 输出示例.md
```

## 许可证

MIT License，详见 [LICENSE](./LICENSE)。
