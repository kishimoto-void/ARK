ARK

Adaptive Reservoir Kernel

ARK is an experimental framework for resilience, recovery, and possibility preservation.

Unlike traditional systems that optimize for a fixed goal, reward function, or value hierarchy, ARK focuses on maintaining and utilizing a reservoir of possibilities.

The central idea is simple:

«Durability emerges from preserving possibilities.
Adaptability emerges from selecting among them.»

---

Core Concepts

Reservoir

ARK maintains a graph of states, experiences, and relationships.

Instead of treating unused paths as waste, ARK preserves alternative routes, latent structures, and recovery candidates as a possibility reservoir.

The reservoir acts as a store of future options.

---

Recovery

When damage occurs, ARK attempts to recover functionality using the remaining structure.

Recovery is not based on restoring an exact previous state.

Instead, ARK searches for viable alternatives within the reservoir.

This allows the system to remain operational even when parts of the original structure are lost.

---

Prepared State

A system can accumulate latent structures before they are needed.

These structures may not provide immediate utility.

However, they increase the probability of successful recovery under future damage.

ARK treats these latent structures as a Prepared State.

---

Possibility Reservoir

Not every useful path is immediately utilized.

Some paths remain dormant for long periods.

ARK preserves these dormant possibilities and tracks their eventual usefulness.

The working hypothesis is:

«The value of a possibility is not determined only by its formation,
but also by its survival and future utilization.»

---

## ProtoArk v1.1 (2026-06-25) - Possibility Ark Prototype

**思想転換の到達点**:
- VoidCore → Ark-P → Ark-PR → **ProtoArk**

**ProtoArkの核心**: 「未来の多様性を維持・拡大できる場所はどこか」

未来は制約から生まれる。
Ark起動時・回復計画時に制約を鑑みながら、可能性空間を運ぶ。

### v1.1 改良点
- **BranchのProtoArkメトリクス強化**: reach_preservation, reservoir_value, predicted_delta, constraint_risk を追加。到達可能性最儦先で評価。
- **lookahead / propose_next_trunk 本格化**: 3手先探索で到達可能性・予測信頼・制約リスクを考慮した幹候補選定。
- **ark_advance() 新規追加**: 幹前進 + ロールバックポイント記録で、単一回復ではなく「良い未来方向へ可能性空間を運びながら前進」を実現。
- **_bfs_recoveryへの制約統合**: 制約違反中は「到達可能性を狭める選択」を強くペナルティ。
- **忠実実験ハーネス**: 220ステップ・ damage 12回の忠実実行。主要メトリクスを定量追跡。

### 忠実実験結果 (seed=20260625)
- **avg_reach_preservation_proxy: 0.952** (min 0.600) — ダメージ後も多様性を高いレベルで維持
- **final_diversity_ratio: 0.868** — 到達可能ノード / 全ノード
- **ark_advance 成功率: 1.0** (24回 / 24回) — 到達可能性を損なわず幹前進
- **avg_prediction_error: 3.4657** — bias/variance/reach 3軸予測器が学習進行
- **constraint_violations 累計: 0** — 制約違反時も到達可能性最儦先の選択が機能

**ProtoArkは「壊れたら戻る」から「良い未来を残せる場所へ多様性を運ぶ」への移行を実証した。**

---

Architecture

ARK separates recovery from decision making.

ARK Core

Responsibilities:

- State preservation
- Reservoir maintenance
- Damage handling
- Recovery execution
- Structural tracking

ARK Core does not decide what is important.

It only maintains what remains possible.

---

Operators

Operators are interchangeable decision criteria.

An Operator does not represent values, emotions, preferences, or goals.

Instead, it applies a mechanical selection criterion to the available possibilities.

Examples:

- Stability Operator
- Exploration Operator
- Resilience Operator
- Learned Operator

Different Operators may choose different recovery paths from the same reservoir.

---

Research Direction

Current research focuses on four questions:

1. How are possibilities formed?
2. How long do they survive?
3. How often are they utilized?
4. Which decision criteria produce the most resilient outcomes?

Future versions may introduce:

- Utilization tracking
- Survival analysis
- Learned Operators
- Utility-driven recovery
- Geometry-aware resilience mechanisms

---

Philosophy

ARK is not designed around fixed values.

It is designed around the interaction between:

- Possibility Preservation
- Recovery
- Mechanical Decision Criteria

The hypothesis behind ARK is that resilience does not emerge from a single optimal solution.

It emerges from maintaining many viable possibilities and selecting among them when needed.

---

Status

Experimental Research Project

ProtoArk v1.1 integrated (2026-06-25).
Full source and experiment logs available in research workflow.

 ark_p.py : ProtoArk v1.1 implementation with faithful 220-step damage/recovery/advance experiment.
