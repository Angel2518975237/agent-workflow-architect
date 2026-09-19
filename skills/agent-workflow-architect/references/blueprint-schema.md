# Agent Workflow Blueprint

Blueprint 是持续更新的设计与验证档案，不替代运行时任务存储或业务系统的权威状态，也不是要求产品经理手工填写的技术表格。Codex 从对话、项目文件和验证结果中补齐，并明确标记证据状态。

## 什么时候使用

需要持续档案且流程简单时使用精简版；单次低风险请求可不创建。

存在多 Agent、共享状态、敏感数据、资金、审批等待、长时间运行、不可逆动作或生产发布审查时，按风险选用完整版的相关部分。

## 证据标记

沿用 [证据与验收](evidence-and-acceptance.md) 的统一语义：已验证、假设、候选、冲突待解、已否决、已失效；业务决定单列决定者与版本，待验证项单列方法与负责人。风险附具体机制、影响和证据。不能用“用户已确认”同时代表事实成立、质量通过和操作授权。

以下是可裁剪的设计模板，不是运行时 JSON Schema；枚举式占位在实际项目中需选定值、明确类型与合法状态转换。只填写适用项，不为填表创造流程。

## 精简版

```markdown
# Agent Workflow Blueprint：项目名

## 目标
- 业务问题：
- 使用者：
- 成功指标与验收者：
- 本期不做：

## 最短流程
触发 → 输入 → 判断 → 动作 → 结果验证 → 失败处理

## 责任边界
| 环节 | Agent | 确定性代码 | 工具 | 真人 |
|---|---|---|---|---|

## 关键工具
| 工具 | 前置条件 | 副作用 | 成功判定 | 失败处理 |
|---|---|---|---|---|

## 主要风险与测试
| 场景 | 影响 | 保护 | 验证证据 |
|---|---|---|---|

## 用户控制（按需）
- 用户看到的阶段、等待原因和依据：
- 可用动作与生效条件：
- 已有授权、需要决定的事项：

## 当前状态
- 已完成：
- 待决定：
- 待验证：
- 下一步：
```

## 完整版

```yaml
project:
  goal: ""
  users: []
  success_metrics: []
  in_scope: []
  out_of_scope: []
  release_stage: concept | prototype | pilot | production

business:
  trigger: ""
  authoritative_inputs: []
  rules: []
  decision_points: []
  human_roles: []
  completion_condition: "引用下方业务完成条件"
  cancellation_and_exceptions: []

product:
  task_record: [] # 目标、任务/计划版本、输入引用、依赖、归属、产物与尝试记录
  lifecycle_and_transition_guards: []
  waiting_reasons: []
  external_action_states: [] # 与生命周期及验收分开
  progress_and_evidence_views: []
  user_actions_and_preconditions: []
  goal_revision_and_invalidation: ""
  background_execution_and_notifications: ""
  takeover_and_return_to_automation: ""

evidence_and_acceptance:
  claim_records_and_provenance: []
  comparability_and_conflict_resolution: []
  artifact_acceptance_contracts: [] # 版本、标准、证据、验收者、退回路径
  business_completion_conditions: []
  user_acceptance_required_when: ""
  evidence_access_and_retention: ""

authorization:
  grants_and_delegation_scope: []
  action_previews_and_approval_binding: []
  expiry_revocation_and_execution_recheck: ""

architecture:
  agents:
    - name: ""
      responsibility: ""
      inputs: []
      outputs: []
      read_scope: []
      write_scope: []
      tools: []
      stop_conditions: []
  coordination: # 多 Agent 时补充；单 Agent 可省略
    topology: single | independent | centralized | decentralized | hybrid
    rationale_and_alternatives: []
    decomposition_evidence: []
    pattern: "候选、验证、修订如何推进；与角色分开描述"
    baseline_and_comparison: []
    handoff_contracts: []
    acceptance_gates: [] # 引用上方验收契约，定义阻断下游的控制路径
    invalidation_and_late_result_policy: ""
    rejected_routes_and_revisit_conditions: []
    budget_owner: ""
    global_limits_and_enforcement: [] # 并发、轮次、工具、上下文、时间、费用
    budget_reservation_and_recovery: ""
    stop_and_degrade_conditions: []
  deterministic_components: []
  state_owners: []
  workflow_dag: []
  human_gates: []

tools:
  contracts:
    - name: ""
      preconditions: []
      effects: read | workspace_write | external_write | irreversible
      success_signal: ""
      failure_signals: []
      idempotency: ""
      timeout_resolution: ""
      authorization_ref: ""
      approval: ""

reliability:
  failure_matrix: []
  retry_policies: []
  compensations: []
  checkpoints: []
  worker_ownership_and_stale_writer_protection: [] # 多执行者接管时适用
  human_escalation: []
  budgets_and_circuit_breakers: []

delivery:
  implementation_status: []
  tests_and_evidence: []
  observability: []
  unresolved_risks: []
  release_decision: releasable | limited_pilot | blocked
  next_review_condition: ""
```

## 维护规则

- 重要实现变更同步更新对应 Blueprint 项，不另建互相冲突的事实版本。
- 测试结果更新“证据”，不能偷偷改变业务规则。
- 用户修正优先于旧推断；保留必要的变更理由和影响。
- 完成事项不能仅靠自报，附运行、测试或权威状态证据。
- Blueprint 不保存无关聊天、密钥或不必要的敏感原文。

## 阶段交付

- 业务澄清：目标、对象、指标、范围和待决定项。
- 产品与架构设计：任务模型、状态/动作表、证据展示、责任边界、流程图和风险。
- 工具编排：工具契约、调用顺序、审批和结果校验。
- 实施：代码状态、测试证据和未验证项。
- 审查：分级发现、修正顺序和发布结论。
