# Agent Workflow Blueprint

Blueprint 是持续更新的工程真相来源，不是要求产品经理手工填写的技术表格。Codex 从对话、项目文件和验证结果中补齐，并明确标记证据状态。

## 什么时候使用

使用精简版，当流程简单、可逆、单 Agent、没有敏感数据或高风险外部写入。

使用完整版，当存在多 Agent、共享状态、敏感数据、资金、审批等待、长时间运行、不可逆动作或生产发布审查。

## 证据标记

- `[已确认]`：用户明确决定，或有代码、配置、权威工具返回和测试证明。
- `[推断]`：有依据但尚未确认；不能自动固化为业务规则。
- `[待决定]`：需要业务负责人取舍。
- `[待验证]`：可通过检查或实验确认。
- `[风险-级别]`：有具体失败机制和影响。

每项关键决定尽量附来源、日期或验证方法。

## 精简版

```markdown
# Agent Workflow Blueprint：项目名

## 目标
- 业务问题：
- 使用者：
- 成功指标：
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
  completion_condition: ""
  cancellation_and_exceptions: []

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
      approval: ""

reliability:
  failure_matrix: []
  retry_policies: []
  compensations: []
  checkpoints: []
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
- 架构设计：责任边界、状态所有者、流程图和风险。
- 工具编排：工具契约、调用顺序、审批和结果校验。
- 实施：代码状态、测试证据和未验证项。
- 审查：分级发现、修正顺序和发布结论。
