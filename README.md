# Trading_Bot_using_Reinforcement_learning
This repository contains the python code for the implementation of a trading bot using Reinforcement Learning Algorithms.
A reinforcement learning problem is mathematically modelled as a Markov Decision Process(which follows the Markov Assumption i.e the next state depends only on the immediate previous state),the Main elements in which include: 1)Agent 2)Environment
Apart from these there are several other elements which help us to describe the interaction between agent and environment namely:-1)Episode 2)State 3)Action 4)Reward 5)Return 6)Q function 7) policy etc. some of which I will describe them below.
**AGENT**:- The job of the agent is to interact with the environment and learn to maximise the expected returns through experience.
**ENVIRONMENT**:- The simulation that the agent interacts with. In an MDP, the most general environment is modelled using the state-transition probability i.e p(s',r|s,a).
**STATE**:- A particular configuration of the environment.(Maybe discrete or infinite.)
**EPISODE**:- A sequence of all successful states(which leads to maximising the return) after which the simulation is concluded.
**REWARD**:- A value associated with each state.
**Action**:- Performing a step that leads to another state and getting a reward.
**Policy**:- A strategy that the agent uses to identify which action it will perform next using only the current state.Its sort of a function or mapping.Usually probabilistic(converted from vectors using softmax function)in nature to allow the agent to perform stochastic actions(fancy word for exploring😁). It is represented as pie(a|s).
**Return**:- Sum of all future rewards.
**SPACES**:- Set of all posiible states/actions is called a/an State/Action Space.
**State-Value Function**:- Conditioned that we arrive on a particular state, it is the expected value to the return.
**Bellman Equation**:- The mathematical equation, the solution for which solves the problem of our MDP.We possibly know the probability distribution of policies and the state-transitions in the Bellman equation so, it just boils down to a linear equation. 
#When the state encapsulates the complete information about the environment then we use deterministic rewards and policies. Other we represent them as probabilties to account for the loss of info for e.g:- We cant deterministically predict the next move by another chess player.
#Discout Factor:- For an Infinite Horizon MDP(or otherwise also), the further you go into the future the harder it is to predict, therefore we care about maximizing our rewards now.(gamma is a hyperparameter close to 1 for e.g:-0.99). Using this we can define the return recursively as G(t)=R(t+1)+gamma*G(t+1).
#Finding the value function for a given policy is called the **Prediction Problem**.This one type of problem in RL, the other being the **Control Problem** in which we have to find the optimal policy pie which yields the maximum value function(In this project, this is the problem that we would be solving).
