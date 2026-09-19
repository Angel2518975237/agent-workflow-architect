# Agent Workflow Architect

作为工作流技术架构师，核心任务是帮助不懂技术的产品经理，把业务需求设计成可落地的 多Agent 工作流。

它帮助你判断是否需要 Agent、如何拆分任务，以及怎样组织协作、工具、数据、权限、状态、验收和异常恢复。产品交互与用户控制围绕架构设计展开；实现、调试和上线审查在用户提出相应需求时进入。它会解释技术取舍、检查现实条件，并给出具体修正。

这是一套工作指引，运行时能力仍需在具体产品中实现。

## 一套贯穿产品与工程的模型

设计围绕六个问题展开：要完成什么、谁负责、依据是什么、可以做什么、现在做到哪里、怎样证明完成或安全退出。

这些问题共用任务标识、输入版本、证据、权限和验收条件。用户界面、Agent 交接、工具执行与后台恢复由此形成一致的行为，而不是各自维护一套“完成”定义。

| 你要解决的问题 | Skill 帮助形成的结果 |
|---|---|
| 业务想法是否值得做、依赖是否真实 | 明确的目标、完成条件、现实约束与最薄业务闭环 |
| 用代码、一个 Agent 还是多个 Agent | 基于依赖、验收、质量与总成本的架构选择 |
| 用户怎么看进度、改方向、接管 | 任务模型、状态与动作表，以及对应的后台条件 |
| 怎样区分事实、猜测和建议 | 带来源与版本的主张、冲突处理与可追溯结果 |
| Agent 能做什么、何时需要确认 | 有范围和有效期的授权、具体行动预览与执行前校验 |
| 如何协作、合并结果并控制预算 | 交接契约、独立验收、退回路径、全局预算和停止条件 |
| 超时、中断或部分失败怎么办 | 保留有效成果、只重试必要步骤、对账、补偿与接管 |
| 方案怎样落实并判断可发布 | 实现、可观察测试证据、运营指标与剩余风险 |

## 它怎样作判断

**先定义业务完成，再选择架构。** 简单任务直接做；并行拆分需要相对独立的输入、可单独验收的子结果和足够收益。为权限隔离或独立复核拆分也可能合理，但要说明额外成本。多步骤和多工具不自动意味着多 Agent。

**让状态驱动交互。** 任务生命周期、等待原因、外部动作结果和产物验收分别记录。用户能理解哪些工作已保留、哪里受阻、能采取什么动作；暂停、取消和关闭页面不被描述成已经撤销外部影响。

**把事实、决定与授权分开。** 用户可以决定范围和接受风险，但认可某个答案不证明它为真。关键结论能够追溯到原始材料；合并前对齐对象、口径、时间与版本，保留未解决的冲突。

**按风险设计控制。** 已有授权仍有效且覆盖当前操作时继续执行；需要批准时，先提供具体目标、参数、影响与可逆性的可审阅预览。授权过期、撤销或动作超出原范围时，运行时阻止执行。

**让验收真正影响下一步。** 执行者自报完成只进入待验收。必要的 Reviewer 能读取原始材料、指出未通过条件并阻止下游；综合后的新结果重新验证。开放问题可使用候选、质疑、综合与有限迭代，并保留失败路线。

**把恢复作为可用能力。** 局部失败不抹掉所有成果；外部动作未知先查询，不能盲目重试或补偿。改目标与人工接管会改变版本和写入归属，旧结果不能覆盖新状态。全局预算覆盖委派、审查和重试。

## 一个贯穿场景

用户已批准发布版本 A，但发布请求超时。产品应显示“发布结果待核实”，保留已通过的构建和测试产物，提供状态查询或人工接管。它不能直接显示“发布失败”并鼓励再次发布。

按原请求号核实后，若确认已部署，则继续健康验证；若确认未执行且授权仍有效，可安全重试；若仍未知，则保留待处理状态。如果用户把目标改成版本 B，原本针对 A 的批准不能直接套用。最终是否完成由预先定义的业务验收条件决定。

## 使用方式

用户交互通常从描述目标开始：

1. 用户说业务目标或当前问题，Skill 结合已有资料，只追问影响方案的关键缺口。
2. 先判断代码、单 Agent 或多 Agent 的适用性，再设计任务、依赖、状态、工具、权限与验收。
3. 给出明确推荐、取舍与异常路径；复杂项目维护一份持续更新的 Blueprint。
4. 用户补资料或改目标时，更新受影响的设计与产物；需要实施时继续修改和验证。
5. 交付方案或实现结果，说明依据、已验证项和仍待验证的部分。

简单问题直接回答，不强制走完整流程。可以这样开始：

```text
$agent-workflow-architect
我要做一个行业研究产品，用户可以中途补资料、暂停和修改范围。
帮我设计任务、证据展示、协作方式和验收，先判断是否需要多 Agent。
```

```text
用户取消任务后，后台偶尔还会写入数据。请检查状态、权限和接管机制，
给出修正并验证；不要只改按钮提示。
```

```text
我们准备上线 Agent 产品。请审查现有实现、关键失败路径与运营条件，
区分已经验证和仍缺证据的部分。
```

咨询交付建议与设计；实施请求会推进修改和验证。设计多 Agent 产品不等于默认在当前任务中启动多 Agent。

## 安装

```bash
git clone https://github.com/Angel2518975237/agent-workflow-architect.git
mkdir -p ~/.codex/skills
cp -R agent-workflow-architect/skills/agent-workflow-architect ~/.codex/skills/
```

将最新版完整的 [`skills/agent-workflow-architect`](skills/agent-workflow-architect) 目录放入 Codex 的 skills 目录。更新已有安装时先备份；重新打开任务以读取更新后的指令。

## 按需加载的结构

入口是 [SKILL.md](skills/agent-workflow-architect/SKILL.md)。参考文件按问题加载，不在每次请求中全部读入：

| 部分 | 参考文件 |
|---|---|
| 路由、沟通与现实条件 | `routing.md`、`communication-style.md`、`business-reality-check.md` |
| 任务、状态与用户控制 | `task-decomposition.md`、`product-task-model.md` |
| 证据、冲突与完成条件 | `evidence-and-acceptance.md` |
| 架构与协作 | `agent-architecture.md`、`multi-agent-coordination.md` |
| 工具、授权与恢复 | `tool-orchestration.md`、`resilience.md` |
| 评估、实现与审查 | `coordination-evaluation.md`、`implementation.md`、`architecture-audit.md` |
| 项目设计档案 | `blueprint-schema.md` |

Blueprint 记录设计与验证状态，不替代后台任务存储。简单低风险请求不强制建立完整蓝图、状态平台、审批流或实验体系。

## 验证与适用边界

本次版本进行 Skill 结构、内部引用、YAML 模板和仓库补丁检查，并人工审阅跨文件规则的一致性。[协作与产品评估](skills/agent-workflow-architect/references/coordination-evaluation.md) 包含基线比较、运营指标口径和 14 类使用/故障场景。

场景清单是可复用的验证方案，不代表已经运行的独立 Agent 测试或生产验证；旧版本的 159 / 160 分不适用于本次版本。运行时权限、状态存储、预算和后台持续执行仍需在具体产品中实现与测试。

## 方法来源

结合用户提供的多 Agent 工程与产品设计原则，保留单 Agent 优先评估、证据与控制边界。Google Research 和 Antigravity Teamwork 的原始参考及适用限制见 [评估来源](skills/agent-workflow-architect/references/coordination-evaluation.md)。实验中的比例、能力阈值与产品能力不直接转成所有项目的通用规则。

原项目亦参考 [OpenAI Agents SDK](https://github.com/openai/openai-agents-python)、[LangGraph](https://github.com/langchain-ai/langgraph)、[Microsoft Agent Framework](https://github.com/microsoft/agent-framework)、[Everything Claude Code](https://github.com/affaan-m/everything-claude-code)、[Agent Skills for Context Engineering](https://github.com/addyosmani/agent-skills) 和 [wshobson/agents](https://github.com/wshobson/agents) 的组织方式与设计思想。此 Skill 不依赖这些项目运行。

## 贡献与许可

欢迎提供真实失败案例、产品交互缺口、证据追溯问题或可复现的验证场景。

[MIT](LICENSE) © 2026 Angel
