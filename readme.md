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

For a given policy \( \pi \), the **state value function** \( V(s) \) satisfies the following recursive relation:

\[ V(s) = \mathbb{E}_\pi \left[ R_t + \gamma V(S_{t+1}) \mid S_t = s \right] \]

where:

- \( V(s) \) is the value of state \( s \)
- \( R_t \) is the immediate reward at time \( t \)
- \( \gamma \) is the discount factor \( (0 \leq \gamma \leq 1) \)
- \( S\_{t+1} \) is the next state
- The expectation is taken over all possible next states under policy \( \pi \)

This equation expresses that the value of a state is the expected return starting from that state and following the policy \( \pi \).

### Bellman Equation for Action Value Function

Similarly, for the **action value function** \( Q(s, a) \), the Bellman equation is given by:

\[ Q(s, a) = \mathbb{E}_\pi \left[ R_t + \gamma Q(S_{t+1}, A\_{t+1}) \mid S_t = s, A_t = a \right] \]

where:

- \( Q(s, a) \) represents the value of taking action \( a \) in state \( s \)
- \( A\_{t+1} \) is the action taken in the next state

This equation describes that the value of an action is the expected reward plus the discounted future value of subsequent actions.

### Importance of the Bellman Equation

- **Foundation of Reinforcement Learning**: Used in value iteration and policy evaluation.
- **Dynamic Programming Basis**: Forms the backbone of algorithms like **Value Iteration** and **Policy Iteration**.
- **Q-Learning & Deep RL**: Used in **Q-learning**, **Deep Q Networks (DQN)**, and **Actor-Critic methods**.
- **Optimality Principle**: Helps in deriving the **Bellman Optimality Equation**, which leads to finding the optimal policy.

The Bellman Equation is a powerful tool that enables efficient decision-making in uncertain environments by breaking down complex problems into recursive relationships.
