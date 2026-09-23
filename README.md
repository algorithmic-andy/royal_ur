# royal_ur

# Royal Ur: Self-Play Across Computational Environments

> **Preliminary research direction**

## Overview

Most self-play reinforcement learning experiments hold the environment fixed and ask how agents improve through repeated interaction with it.

This project explores a different question:

> **What happens when the environment itself becomes part of the learning problem?**

Rather than training agents exclusively within one fixed game, the goal is to construct a **family of related computational environments**, systematically vary their rules or structure, and study whether self-play produces strategies that generalize beyond the environments encountered during training.

The **Royal Game of Ur** is the initial testbed. Its relatively simple rules make it possible to generate many controlled variants while retaining a meaningful strategic objective.

A longer-term extension is to move beyond variants of a single game and investigate transfer across **structurally different environments**, such as American Mahjong.

---

## Research Question

Can self-play reinforcement learning produce strategies that generalize across a space of computational environments rather than specializing to a single environment?

More specifically:

* Does decomposition of reward information improve model performance?
* How much environmental diversity is useful before it becomes disruptive?
* Can agents transfer knowledge to previously unseen environments?
* Which properties of an environment determine whether learned strategies transfer?
* Can the distribution of training environments itself be optimized?

---

## Initial Environment: Royal Game of Ur

The Royal Game of Ur provides a convenient starting point because its rules can be parameterized without requiring an entirely new learning system for every experiment.

Potential environment parameters include:

* Board geometry
* Board size
* Number and location of rosettes
* Rosette effects
* Movement rules
* Entry rules
* Capture rules
* Number of pieces
* Dice distribution
* Opponent strategy

This creates a potentially large space of related environments:

$$
E_\theta,\qquad \theta \in \Theta
$$

where each value of \(\theta\) defines a particular computational environment.

The agent is therefore not necessarily learning one game. It is learning within a **distribution of games**.

---

## Experimental Framework

A simple progression could compare increasingly broad forms of training.

| Training                   | Evaluation         | Question                                                     |
| -------------------------- | ------------------ | ------------------------------------------------------------ |
| \(E_1\)                    | \(E_1\)            | Can agents learn the environment?                            |
| \(E_1\)                    | \(E_2\)            | Does a strategy transfer to a related environment?           |
| \(E_1,\ldots,E_k\)         | Seen environments  | Does environmental diversity affect learning?                |
| \(E_1,\ldots,E_k\)         | Unseen \(E_{k+1}\) | Can agents generalize to new environments?                   |
| \(E_\theta\sim P(\theta)\) | New \(E_\theta\)   | Does training over a distribution produce robust strategies? |

The goal is not simply to maximize performance in one game, but to study the relationship between:

**environmental variation → self-play → strategy formation → transfer**

---

## Beyond One Game

A particularly interesting extension is to move from **within-game variation** to **cross-game variation**.

### American Mahjong

American Mahjong provides a substantially different computational environment from Royal Ur.

Instead of modifying the rules of one board game, the research could investigate whether agents can learn across environments with fundamentally different structures, action spaces, information patterns, and strategic objectives.

Potential sources of variation include:

* Tile distributions
* Hand construction rules
* Scoring systems
* Winning conditions
* Special hands
* Joker rules
* Discard mechanics
* Number of players
* Information available to each agent
* Rule variations between Mahjong implementations

This creates a hierarchy of environmental generalization:

$$
\text{Same Environment}
\rightarrow
\text{Game Variants}
\rightarrow
\text{Different Games}
$$

Royal Ur would therefore serve as a controlled starting point, while American Mahjong could provide a substantially different test of the broader hypothesis.

---

## A Possible Research Program

The project could eventually investigate three levels of generalization.

### 1. Intra-environment learning

Train and evaluate within the same environment.

$$
E_1 \rightarrow E_1
$$

This provides the baseline for conventional self-play.

### 2. Intra-family generalization

Train on variants of one environment and evaluate on unseen variants.

$$
\{E_{\theta_1},\ldots,E_{\theta_k}\}
\rightarrow
E_{\theta_{k+1}}
$$

For example, an agent could train on several Royal Ur variants and then encounter a new board configuration or dice distribution.

### 3. Cross-environment generalization

Train across structurally different environments and evaluate on environments that were not directly encountered during training.

$$
\{E_1,\ldots,E_k\}
\rightarrow
E_{\text{new}}
$$

This is the more ambitious direction.

The central question becomes whether self-play can learn **principles of decision-making** that transfer across computational environments rather than merely memorizing environment-specific strategies.

---

## Why Self-Play?

Self-play is particularly interesting in this setting because it removes the need to specify a fixed opponent strategy.

Agents can generate their own experience while simultaneously adapting to the strategies produced by other agents.

This creates a potentially open-ended process:

$$
\text{Environment}
\rightarrow
\text{Self-Play}
\rightarrow
\text{Strategy}
\rightarrow
\text{New Environment}
\rightarrow
\text{New Strategy}
\rightarrow \cdots
$$

The environment distribution could therefore become an additional experimental variable.

One possible future direction is to ask whether environments can be selected **because they are informative**, rather than sampled uniformly.

---

## Research Hypotheses

Initial hypotheses include:

1. **Structured variation may improve generalization.**
   Training across related environments may discourage strategies that depend too heavily on environment-specific details.

2. **Environmental diversity may have an optimal range.**
   More variation is not necessarily better. Extremely heterogeneous environments could make learning substantially more difficult.

3. **Some environments may transfer better than others.**
   Structural similarities between environments may predict the degree of strategic transfer.

4. **Unseen environments provide a stronger test than held-out games.**
   Performance on environments never encountered during training may reveal whether agents learned transferable strategies rather than environment-specific policies.

5. **The environment distribution may itself be learnable.**
   Future experiments could investigate whether training environments can be selected adaptively to maximize learning or generalization.

---

## Potential Measurements

Possible measurements include:

* Win rate
* Expected reward
* Learning speed
* Sample efficiency
* Strategy diversity
* Transfer performance
* Performance degradation on unseen environments
* Sensitivity to environment parameters
* Policy similarity across environments
* Robustness to rule perturbations

A useful quantity for cross-environment experiments could be a transfer matrix:

$$
T_{ij}
=
\text{performance on }E_j
\text{ after training on }E_i.
$$

This would allow the environments themselves to be studied as a network of transferable strategies.

---

## Longer-Term Direction

The ultimate goal is not to build a particularly strong Royal Ur or Mahjong agent.

The broader research direction is to investigate **learning systems that operate over spaces of computational environments**.

Games provide convenient experimental laboratories because environments can be simulated cheaply, rules can be modified systematically, and outcomes can often be evaluated objectively.

The same framework could potentially extend beyond games to:

* Optimization problems
* Constraint satisfaction
* Search problems
* Scheduling
* Combinatorial environments
* Simulated economic systems
* Algorithmic environments

This raises a broader question:

> **Can an agent learn how to reason across environments rather than merely within an environment?**

---

## Current Status

This repository currently represents a **preliminary research direction** rather than a completed empirical study.

The initial work is focused on developing the research framework, identifying useful environment parameters, and determining how to construct controlled experiments.

No empirical claims are made at this stage.

The immediate objective is to implement a minimal Royal Ur environment, establish a self-play baseline, and then introduce controlled environmental variation.

---

## Planned Experiments

### Phase 1 — Royal Ur

* Implement a reproducible Royal Ur environment.
* Train agents through self-play.
* Establish baseline learning curves.
* Create controlled rule variants.
* Measure transfer between variants.

### Phase 2 — Environment Generalization

* Generate families of Royal Ur environments.
* Train over distributions of variants.
* Evaluate on unseen environments.
* Construct environment-to-environment transfer matrices.
* Study the relationship between environment similarity and transfer.

### Phase 3 — Cross-Game Extension

Investigate whether the framework can extend to a structurally different environment such as **American Mahjong**.

The purpose would not necessarily be direct policy transfer between games. Instead, the experiment could investigate whether a common learning framework can discover useful representations or decision-making patterns across substantially different computational environments.

### Phase 4 — Adaptive Environment Generation

A longer-term possibility is to allow the learning system to influence which environments are generated next.

Instead of:

$$
E_t \sim P(E),
$$

consider:

$$
E_t \sim P(E\mid\text{agent state}),
$$

so that the environment distribution becomes part of the learning process.

This could turn the project from fixed self-play into a form of **adaptive computational curriculum generation**.

---

## Repository Structure

The repository is intentionally kept lightweight while the research direction is being developed.

```text
royal_ur/
├── README.md
├── environment/
├── agents/
├── experiments/
├── evaluation/
└── research/
```

The structure may change as the experimental framework becomes clearer.

---

## Research Note

A one-page research note describing the motivation and proposed framework is included in the repository:

**Beyond Self-Play: Learning Across a Space of Computational Environments**

The note is intentionally presented as a preliminary research direction rather than a completed research paper.

---

## Keywords

**Self-Play Reinforcement Learning · Environment Generalization · Emergent Strategy**

---

## License

This project is currently exploratory research. Licensing and publication details will be added as the implementation develops.
