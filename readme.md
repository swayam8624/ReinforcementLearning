# Reinforcement Learning

## Elements common to all control tasks -->

- States , Actions , and Rewards at Time t
- Agents -- algorithms carrying out task in this case
- Environment -- not in control of agents (eg - gravity , opponents move)

### Markov Decision Process (MDP) -->

`Discrete Time Stochastic control Process`

- Extension of Markov chain
- time moves forwards in finite intervals
- future states depend only partially on actions taken
- it is based on decision making to reach the target state

![alt text](image.png)

`(S.A.R.P.) -- Possible States , Set of Actions in each task , Set of Rewards for each (s,a) pair, PRobablities of passing from one state to another when taking each action`

_The next state depends only on the current state , not on previous states as they have no memory , if a process meets this property , ther are called Markov Process_
