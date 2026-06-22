---
source: sources/wiki-Reinforcement_learning.md
source_url: https://en.wikipedia.org/wiki/Reinforcement_learning
---

## Reinforcement Learning: Foundations, Algorithms, and Key Methods

Reinforcement learning (RL) is a machine learning paradigm where an intelligent agent learns to take actions in a dynamic environment to maximize cumulative reward. Unlike supervised learning (which uses labeled data) or unsupervised learning (which finds patterns in unlabeled data), RL learns through interaction with an environment, balancing exploration of new actions against exploitation of known good actions. The problem is typically formalized as a Markov decision process (MDP).

## Key Concepts

- **Agent-environment loop**: At each discrete time step *t*, the agent observes state S_t and reward R_t, selects action A_t, then the environment transitions to S_{t+1} and produces reward R_{t+1}
- **Policy (π)**: A mapping from states and actions to probabilities — π(a,s) = Pr(A_t = a | S_t = s). Can be stochastic or deterministic
- **State-value function V_π(s)**: Expected discounted return starting from state *s* and following policy π — estimates "how good" it is to be in a given state
- **Action-value function Q_π(s,a)**: Expected discounted return starting from state *s*, taking action *a*, then following π. Knowing Q* alone suffices to act optimally
- **Discounted return G**: G = Σ γ^t R_{t+1} where 0 ≤ γ < 1 is the discount factor; future rewards weighted less than immediate rewards
- **Exploration vs. exploitation dilemma**: Agent must balance trying new actions (exploration) vs. using known-best actions (exploitation); studied extensively via the multi-armed bandit problem
- **ε-greedy exploration**: With probability (1-ε) choose the best-known action (exploit); with probability ε choose a random action (explore)
- **Full vs. partial observability**: If the agent sees the complete state → MDP; if it sees only a subset or noisy observations → Partially Observable MDP (POMDP)
- **Regret**: Difference between agent's performance and optimal agent's performance
- **Stationary policy**: Action distribution depends only on the current state, not history. Optimal policy can always be found among deterministic stationary policies
- **Two sources of RL power**: (1) using samples to optimize performance, (2) function approximation for large environments

## Commands and Syntax

**MDP Formal Definition:**
- State space S, Action space A
- Transition probability: P_a(s, s') = Pr(S_{t+1} = s' | S_t = s, A_t = a)
- Immediate reward: R_a(s, s') after transitioning from s to s' under action a

**Value Function (Bellman-style):**
- V_π(s) = E[Σ_{t=0}^∞ γ^t R_{t+1} | S_0 = s]
- Optimal value: V*(s) = max_π V^π(s)
- Optimal action-value: Q*(s,a) — act optimally by choosing argmax_a Q*(s,a) at each state

**Two main algorithmic approaches:**
1. **Value function estimation** — maintain estimates of expected returns (on-policy or off-policy)
2. **Direct policy search** — search policy space directly

## Relationships

- **Markov Decision Processes**: RL's formal mathematical framework; many RL algorithms use dynamic programming techniques on MDPs
- **Supervised/Unsupervised Learning**: RL is the third paradigm — distinct because it learns from interaction rather than from static datasets
- **Optimal Control Theory**: RL is the learning/approximation counterpart to classical optimal control; called "approximate dynamic programming" or "neuro-dynamic programming" in control literature
- **Multi-armed Bandit**: Simplified RL setting used to study the exploration-exploitation tradeoff in isolation
- **Game Theory, Control Theory, Operations Research, Information Theory**: RL is studied across all these disciplines
- **Function Approximation / Neural Networks**: Enables RL to scale to large/continuous state spaces (foundation of deep RL)
- **POMDP**: Extension of MDP framework when agent has partial observability

## Exam-Relevant Points

- RL is one of **three** ML paradigms (supervised, unsupervised, reinforcement)
- The MDP is defined by four components: **state space S, action space A, transition probabilities P, reward function R**
- The **discount factor γ** must satisfy 0 ≤ γ < 1 to ensure convergence of infinite-horizon returns
- **Knowing Q* is sufficient** to act optimally — no need for a model of the environment
- Optimal policies can always be found among **deterministic stationary policies** (no loss of generality)
- RL does **not** require knowledge of the exact MDP model, unlike classical dynamic programming
- The **exploration-exploitation tradeoff** is fundamental; ε-greedy is the simplest practical method
- **Brute force** policy evaluation fails due to exponential/infinite policy space and high variance of returns
- RL converts both **planning problems** (model available) and **learning problems** (model unknown) into machine learning problems
- Key applications: Go (AlphaGo), robotics, autonomous driving, energy storage, game playing (backgammon, checkers)
- **Value function methods** vs. **direct policy search** are the two main algorithmic families
- **On-policy** methods evaluate/improve the current policy; **off-policy** methods evaluate/improve a different (typically optimal) policy
