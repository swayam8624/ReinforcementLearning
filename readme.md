# Reinforcement Learning

## Common Elements in All Control Tasks

- **States, Actions, and Rewards at Time t**
- **Agent** – The algorithm performing the task
- **Environment** – The external system not controlled by the agent (e.g., gravity, opponent's moves)

## Markov Decision Process (MDP)

### Definition

A **Discrete-Time Stochastic Control Process** that extends a Markov chain by incorporating rewards and actions.

- Time progresses in finite intervals
- Future states depend partially on actions taken
- Decision-making is used to reach the target state

### Key Components (S.A.R.P.)

- **S** – Possible states
- **A** – Set of actions available in each task
- **R** – Set of rewards for each (s, a) pair
- **P** – Probabilities of transitioning from one state to another given an action

A process is called a **Markov Process** if the next state depends only on the current state and not on past states (i.e., it has no memory).

## Types of MDPs

### Based on State Size

1. **Finite MDP** – All sets (states, actions, and rewards) are finite (e.g., route mapping)
2. **Infinite MDP** – At least one state is infinite (e.g., driving a car)

### Based on Duration

1. **Episodic** – The process has a well-defined start and end state
2. **Continuing** – The process continues indefinitely

## Trajectory vs. Episode

- **Trajectory**: The sequence of elements generated as the agent transitions from one state to another

  `τ = S0, A0, R1, S1, A1, R2, S2, A2, R3, S3, ...`

- **Episode**: A complete trajectory from the initial state to the terminal state

## Reward vs. Return

- **Reward (R(t))** – Immediate feedback from an action
- **Return** – The cumulative sum of rewards from a given time (t) until task completion (T)
- The objective is to **maximize long-term rewards**, even if short-term rewards are sacrificed (e.g., strategic moves in chess)

## Discount Factor (γ)

To improve efficiency, returns are modified using a **discount factor** `γ` (gamma), where `γ ∈ [0,1]`.

Formula:

`G₀ (Return from time 0) = R1 + γ*R2 + γ²*R3 + γ³*R4 + ... + γ^(T-t-1) * RT`

## Policy (π(s))

A function that determines what action to take in a given particular state.

`π: S → A`

_A well-optimized policy helps in maximizing long-term returns efficiently._

- **π(a|s)** --> Probability of taking action a in state s
- **π(a)** --> Action a taken in state s

* Can be `Stochastic` -- Taking actions based on probabilities of all actions or `Deterministic` -- taking action based on the given state

## State Value and Action Value

### State Value Function (V(s))

The **state value function** measures how good it is for an agent to be in a given state under a specific policy.

Formula:

`V(s) = E[ G_t | S_t = s ]`

where `E` denotes expectation, and `G_t` is the return starting from state `s` at time `t`.

### Action Value Function (Q(s, a))

The **action value function** measures how good it is to take a particular action in a given state under a specific policy.

Formula:

`Q(s, a) = E[ G_t | S_t = s, A_t = a ]`

The action value function helps in making decisions about the best actions to take in a given state to maximize future rewards.

## Bellman Equation

### Definition

The **Bellman Equation** is a fundamental recursive formula in reinforcement learning and dynamic programming. It expresses the value of a state as the sum of immediate rewards and the discounted value of future states. This equation helps in evaluating policies and optimizing decisions in Markov Decision Processes (MDPs).

### Bellman Equation for State Value Function

For a given policy pi , the **state value function** V(s) satisfies the following recursive relation:

V(s) = Exp[ R_t + gamma V(S_{t+1})| S_t = s ]

where:

- V(s) is the value of state s
- R_t is the immediate reward at time t
- gamma is the discount factor (0 \leq \gamma \leq 1)
- S{t+1} is the next state
- The expectation is taken over all possible next states under policy \pi

This equation expresses that the value of a state is the expected return starting from that state and following the policy \( \pi \).

### Bellman Equation for Action Value Function

Similarly, for the **action value function** Q(s, a) , the Bellman equation is given by:

Q(s, a) = Exp[ R_t + \gamma Q(S_{t+1}, A\_{t+1})| S_t = s, A_t = a ]

where:

- Q(s, a) represents the value of taking action a in state s
- A{t+1} is the action taken in the next state

This equation describes that the value of an action is the expected reward plus the discounted future value of subsequent actions.

### Importance of the Bellman Equation

- **Foundation of Reinforcement Learning**: Used in value iteration and policy evaluation.
- **Dynamic Programming Basis**: Forms the backbone of algorithms like **Value Iteration** and **Policy Iteration**.
- **Q-Learning & Deep RL**: Used in **Q-learning**, **Deep Q Networks (DQN)**, and **Actor-Critic methods**.
- **Optimality Principle**: Helps in deriving the **Bellman Optimality Equation**, which leads to finding the optimal policy.

The Bellman Equation is a powerful tool that enables efficient decision-making in uncertain environments by breaking down complex problems into recursive relationships.

# Dynamic Programming in Reinforcement Learning

Dynamic Programming (DP) is a fundamental concept in Reinforcement Learning (RL) that involves breaking down complex problems into simpler subproblems. It is used to solve Markov Decision Processes (MDPs) by leveraging the principle of optimality and the Bellman equation.

## Introduction

Dynamic Programming is a method used to solve problems by breaking them down into simpler subproblems. In the context of Reinforcement Learning, DP algorithms are used to find optimal policies for MDPs by iteratively improving value functions and policies.

## Key Concepts

### Markov Decision Process (MDP)

An MDP is defined by the tuple \((S, A, P, R, \gamma)\), where:

- \(S\): Set of states
- \(A\): Set of actions
- \(P\): Transition probability matrix, \(P(s' | s, a)\)
- \(R\): Reward function, \(R(s, a, s')\)
- \(\gamma\): Discount factor, \(0 \leq \gamma \leq 1\)

### Bellman Equation

The Bellman equation is a recursive decomposition of the value function. For a given policy \(\pi\), the value function \(V^\pi(s)\) satisfies:

\[
V^\pi(s) = \sum*{a} \pi(a|s) \sum*{s'} P(s' | s, a) [R(s, a, s') + \gamma V^\pi(s')]
\]

### Value Function

The value function \(V^\pi(s)\) represents the expected return when starting in state \(s\) and following policy \(\pi\) thereafter.

\[
V^\pi(s) = \mathbb{E} \left[ \sum_{t=0}^{\infty} \gamma^t R_t \mid s_0 = s, \pi \right]
\]

### Policy

A policy \(\pi\) is a mapping from states to actions. It can be deterministic or stochastic.

\[
\pi: S \rightarrow A
\]

## Dynamic Programming Algorithms

### Policy Evaluation

Policy evaluation is the process of computing the value function \(V^\pi\) for a given policy \(\pi\). It involves solving the Bellman equation iteratively.

\[
V*{k+1}(s) = \sum*{a} \pi(a|s) \sum\_{s'} P(s' | s, a) [R(s, a, s') + \gamma V_k(s')]
\]

### Policy Improvement

Policy improvement involves updating the policy \(\pi\) to be greedy with respect to the current value function \(V^\pi\).

\[
\pi'(s) = \arg\max*{a} \sum*{s'} P(s' | s, a) [R(s, a, s') + \gamma V^\pi(s')]
\]

### Policy Iteration

Policy iteration alternates between policy evaluation and policy improvement until convergence to an optimal policy.

1. **Policy Evaluation**: Compute \(V^\pi\) for the current policy \(\pi\).
2. **Policy Improvement**: Update \(\pi\) to be greedy with respect to \(V^\pi\).
3. Repeat until \(\pi\) converges.

### Value Iteration

Value iteration is a dynamic programming algorithm that combines policy evaluation and policy improvement into a single step.

\[
V*{k+1}(s) = \max*{a} \sum\_{s'} P(s' | s, a) [R(s, a, s') + \gamma V_k(s')]
\]

## Formulas

- **Bellman Expectation Equation**:
  \[
  V^\pi(s) = \sum*{a} \pi(a|s) \sum*{s'} P(s' | s, a) [R(s, a, s') + \gamma V^\pi(s')]
  \]

- **Bellman Optimality Equation**:
  \[
  V^_(s) = \max*{a} \sum*{s'} P(s' | s, a) [R(s, a, s') + \gamma V^_(s')]
  \]

- **Q-Function**:
  \[
  Q^\pi(s, a) = \sum\_{s'} P(s' | s, a) [R(s, a, s') + \gamma V^\pi(s')]
  \]

- **Optimal Q-Function**:
  \[
  Q^_(s, a) = \sum*{s'} P(s' | s, a) [R(s, a, s') + \gamma \max*{a'} Q^_(s', a')]
  \]

# Monte Carlo Methods in Reinforcement Learning

Monte Carlo (MC) methods are a class of algorithms in Reinforcement Learning (RL) that rely on repeated random sampling to estimate value functions and optimize policies. Unlike Dynamic Programming (DP), Monte Carlo methods do not require a complete model of the environment and instead learn directly from episodes of experience.

## Introduction

Monte Carlo methods are used in RL to estimate value functions and optimize policies by averaging the returns observed from sampled episodes. These methods are **model-free**, meaning they do not require knowledge of the environment's dynamics (transition probabilities or reward function). Instead, they learn directly from experience.

---

## Key Concepts

### Episodic Tasks

Monte Carlo methods are applicable only to **episodic tasks**, where the agent's interaction with the environment can be divided into episodes that terminate after a finite number of steps.

### Returns

The **return** \(G_t\) is the total discounted reward from time step \(t\) onward:

\[
G*t = R*{t+1} + \gamma R*{t+2} + \gamma^2 R*{t+3} + \dots = \sum*{k=0}^{\infty} \gamma^k R*{t+k+1}
\]

where:

- \(R_t\): Reward at time step \(t\)
- \(\gamma\): Discount factor (\(0 \leq \gamma \leq 1\))

### Value Function Estimation

The value function \(V^\pi(s)\) for a policy \(\pi\) is the expected return when starting in state \(s\) and following \(\pi\):

\[
V^\pi(s) = \mathbb{E}[G_t \mid S_t = s, \pi]
\]

Similarly, the action-value function \(Q^\pi(s, a)\) is the expected return when starting in state \(s\), taking action \(a\), and following \(\pi\) thereafter:

\[
Q^\pi(s, a) = \mathbb{E}[G_t \mid S_t = s, A_t = a, \pi]
\]

### Policy Evaluation

Monte Carlo policy evaluation estimates \(V^\pi(s)\) or \(Q^\pi(s, a)\) by averaging the returns observed from episodes.

### Policy Improvement

Once the value function is estimated, the policy can be improved by making it greedy with respect to the current value function.

---

## Monte Carlo Algorithms

### Monte Carlo Prediction

Monte Carlo prediction is used to estimate the value function \(V^\pi(s)\) or \(Q^\pi(s, a)\) for a given policy \(\pi\). It works by:

1. Generating episodes using policy \(\pi\).
2. Calculating the return \(G_t\) for each state or state-action pair.
3. Averaging the returns to estimate the value function.

For **first-visit MC**, each state's value is estimated using the return from the first time it is visited in an episode. For **every-visit MC**, all visits to a state are used.

### Monte Carlo Control

Monte Carlo control is used to find the optimal policy \(\pi^\*\). It alternates between:

1. **Policy Evaluation**: Estimating \(Q^\pi(s, a)\) using Monte Carlo prediction.
2. **Policy Improvement**: Updating the policy to be greedy with respect to \(Q^\pi(s, a)\).

\[
\pi(s) = \arg\max\_{a} Q^\pi(s, a)
\]

### Exploring Starts

To ensure all state-action pairs are explored, Monte Carlo control often uses **exploring starts**, where every state-action pair has a non-zero probability of being selected as the start of an episode.

### On-Policy vs Off-Policy Methods

- **On-Policy**: Learn about the policy being used to generate episodes (e.g., \(\epsilon\)-greedy policies).
- **Off-Policy**: Learn about a target policy while following a different behavior policy (e.g., Q-learning).

---

## Formulas

1. **Return**:
   \[
   G*t = R*{t+1} + \gamma R*{t+2} + \gamma^2 R*{t+3} + \dots
   \]

2. **Value Function**:
   \[
   V^\pi(s) = \mathbb{E}[G_t \mid S_t = s, \pi]
   \]

3. **Action-Value Function**:
   \[
   Q^\pi(s, a) = \mathbb{E}[G_t \mid S_t = s, A_t = a, \pi]
   \]

4. **Policy Improvement**:
   \[
   \pi(s) = \arg\max\_{a} Q^\pi(s, a)
   \]

5. **Incremental Update Rule**:
   For each episode, update the value function incrementally:
   \[
   V(S_t) \leftarrow V(S_t) + \alpha [G_t - V(S_t)]
   \]

# Temporal Difference Methods in Reinforcement Learning

Temporal Difference (TD) methods are a class of model-free reinforcement learning algorithms that combine ideas from **Dynamic Programming (DP)** and **Monte Carlo (MC)** methods. Unlike Monte Carlo methods, TD methods do not require waiting until the end of an episode to update value estimates. Instead, they update estimates based on **bootstrapping**—using current estimates to improve future estimates.

## Introduction

Temporal Difference methods are **model-free** and **online**, meaning they learn directly from experience without requiring a model of the environment and update estimates after every time step. TD methods are widely used in RL because they are computationally efficient and can be applied to both episodic and continuing tasks.

---

## Key Concepts

### Bootstrapping

Bootstrapping is the process of updating estimates based on other estimates. In TD methods, the value of a state is updated using the observed reward and the estimated value of the next state.

### TD Error

The **TD error** is the difference between the target value (estimated return) and the current estimate. It drives updates to the value function.

\[
\delta*t = R*{t+1} + \gamma V(S\_{t+1}) - V(S_t)
\]

where:

- \(R\_{t+1}\): Immediate reward
- \(\gamma\): Discount factor
- \(V(S_t)\): Current estimate of the value of state \(S_t\)
- \(V(S*{t+1})\): Estimate of the value of the next state \(S*{t+1}\)

### Value Function Estimation

TD methods estimate the value function \(V(s)\) or action-value function \(Q(s, a)\) by iteratively updating their estimates using the TD error.

### Policy Evaluation

TD prediction is used to estimate the value function \(V^\pi(s)\) for a given policy \(\pi\).

### Policy Improvement

Once the value function is estimated, the policy can be improved by making it greedy with respect to the current value function.

---

## TD Algorithms

### TD Prediction

TD prediction is used to estimate the value function \(V^\pi(s)\) for a given policy \(\pi\). The update rule is:

\[
V(S*t) \leftarrow V(S_t) + \alpha [R*{t+1} + \gamma V(S\_{t+1}) - V(S_t)]
\]

where:

- \(\alpha\): Learning rate
- \(\gamma\): Discount factor

### SARSA (On-Policy TD Control)

SARSA is an on-policy TD control algorithm that estimates the action-value function \(Q(s, a)\) and improves the policy iteratively. The name SARSA comes from the sequence of updates: **State, Action, Reward, State, Action**.

The update rule for SARSA is:

\[
Q(S*t, A_t) \leftarrow Q(S_t, A_t) + \alpha [R*{t+1} + \gamma Q(S*{t+1}, A*{t+1}) - Q(S_t, A_t)]
\]

SARSA follows the policy being learned (on-policy) and uses an \(\epsilon\)-greedy strategy for exploration.

### Q-Learning (Off-Policy TD Control)

Q-learning is an off-policy TD control algorithm that directly estimates the optimal action-value function \(Q^\*(s, a)\). It does not depend on the policy being followed, making it off-policy.

The update rule for Q-learning is:

\[
Q(S*t, A_t) \leftarrow Q(S_t, A_t) + \alpha [R*{t+1} + \gamma \max*{a} Q(S*{t+1}, a) - Q(S_t, A_t)]
\]

Q-learning uses the maximum estimated value of the next state, making it more aggressive in pursuing the optimal policy.

---

## Formulas

1. **TD Error**:
   \[
   \delta*t = R*{t+1} + \gamma V(S\_{t+1}) - V(S_t)
   \]

2. **TD Prediction Update**:
   \[
   V(S*t) \leftarrow V(S_t) + \alpha [R*{t+1} + \gamma V(S\_{t+1}) - V(S_t)]
   \]

3. **SARSA Update**:
   \[
   Q(S*t, A_t) \leftarrow Q(S_t, A_t) + \alpha [R*{t+1} + \gamma Q(S*{t+1}, A*{t+1}) - Q(S_t, A_t)]
   \]

4. **Q-Learning Update**:
   \[
   Q(S*t, A_t) \leftarrow Q(S_t, A_t) + \alpha [R*{t+1} + \gamma \max*{a} Q(S*{t+1}, a) - Q(S_t, A_t)]
   \]

5. **Value Function**:
   \[
   V^\pi(s) = \mathbb{E}[R_{t+1} + \gamma V^\pi(S_{t+1}) \mid S_t = s, \pi]
   \]

6. **Action-Value Function**:
   \[
   Q^\pi(s, a) = \mathbb{E}[R_{t+1} + \gamma Q^\pi(S_{t+1}, A_{t+1}) \mid S_t = s, A_t = a, \pi]
   \]

---
