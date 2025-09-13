---
aip: 2
title: Availability-Weighted Reward Mechanism
description: Adjust validator rewards proportionally to their availability score to
  incentivize consistent uptime and reliable participation.
author: Javad Rajabzadeh (@ja7ad)
status: Draft
type: Standard
category: Core
discussion-no: 3
created: 2025-09-13
---

## Abstract

This proposal introduces a mechanism to scale validator rewards based on their
availability score. Validators with higher availability scores will earn a
larger portion of their base reward, while those with lower scores will receive
proportionally reduced rewards. This adjustment aims to incentivize validators
to maintain consistent uptime and reliable participation, thereby improving
network performance and security.

## Motivation

Currently, validator rewards are distributed evenly regardless of their reputation
or availability score, as long as the validator is active in the committee.
This can result in validators with suboptimal availability still receiving the
same reward as highly reliable validators. By linking rewards to availability,
we align economic incentives with the network’s need for dependable
participation, discourage semi-active validators, and create a fairer reward
system based on actual contribution.

## Specification

- **Availability Score**:
   - A value between $0.0$ and $1.0$ representing the validator's recent
    performance and uptime.
   - Scores below $\tau = \frac{2}{3}\;(\approx 0.666667)$ result in temporary
     exclusion from the committee (no rewards).
   - Scores $≥ 0.666667$ are eligible for scaled rewards.

- **Reward Scaling Formula**:
   - Let $base\\_reward$ be the validator's share of the block reward (e.g., if
    the protocol allocates 70% of each block reward to validators and 30% to
    the foundation, then $base\\_reward$ = 0.7 AUM).
   - The adjusted reward is calculated as:

      $$
      reward = base\\_reward × (α + (1 − α) × score)
      $$

   - Where:
      - $α$ = fixed proportion (e.g., 0.5) ensuring a minimum reward floor.
      - $score$ = availability score of the validator (0.0 ≤ score ≤ 1.0).

- **Examples** (with $base\\_reward = 0.7$, $α = 0.5$):
   - $score = 1.0$ → $reward = 0.7 AUM$
   - $score = 0.98$ → $reward = 0.693 AUM$
   - $score = 0.6$ (below $\tau$) → excluded → $reward = 0$
   - $score = 0.0$ (below $\tau$) → excluded → $reward = 0$

This approach ensures validators with excellent availability maximize their
rewards, while poorly performing validators earn less; validators below the
threshold receive no rewards while temporarily excluded.

## Backwards Compatibility

No backward compatibility issues found. Existing reward distribution rules
remain compatible, with only the distribution formula adjusted.

## Test Cases

- Validator $score = 1.0$, $reward = 0.7$
- Validator $score = 0.98$, $reward ≈ 0.693$
- Validator $score = 0.6$ (below $\tau$), $reward = 0$
- Validator $score = 0.0$ (below $\tau$), $reward = 0$
- Validator $score < 0.666667$ and excluded from committee → $reward = 0$

## Security Considerations

- **Sybil Resistance**: Validators may attempt to reset identity to bypass low
  scores. This must be mitigated by slashing, stake requirements, or bonding
  periods.
- **Score Manipulation**: Availability scoring must be robust against
  manipulation and accurately reflect validator performance.
- **Fairness**: Ensures consistent uptime is rewarded but prevents harsh
  penalties that could discourage participation.
- **Network Resilience**: By rewarding reliability, the system promotes a
  stronger validator set and reduces the risk of downtime.
