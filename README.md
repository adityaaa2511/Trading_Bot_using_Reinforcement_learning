# Trading_Bot_using_Reinforcement_learning
This repository contains the python code for the implementation of a trading bot using Reinforcement Learning Algorithms.<br/>
*A **Reinforcement learning** problem is mathematically modelled as a Markov Decision Process(which follows the Markov Assumption i.e the next state depends only on the immediate previous state),the Main elements in which include: 1)Agent 2)Environment.<br/>*
Apart from these there are several other elements which help us to describe the interaction between agent and environment namely:-<br/> 
1)Episode <br/> 
2)State <br/>
3)Action <br/>
4)Reward <br/>
5)Return <br/>
6)Q function <br/>
7) policy etc. <br/>
some of which I will describe below.<br/>
* **AGENT**:- The job of the agent is to interact with the environment and learn to maximise the expected returns through experience.<br/>
* **ENVIRONMENT**:- The simulation that the agent interacts with. In an (yes it should an, not a😁)MDP, the most general environment is modelled using the state-transition probability i.e p(s',r|s,a).<br/>
* **State**:- A particular configuration of the environment.(Maybe discrete or infinite.)<br/>
* **Episode**:- A sequence of all successful states(which leads to maximising the return) after which the simulation is concluded.<br/>
* **Reward**:- A value associated with each state.<br/>
* **Action**:- Performing a step that leads to another state and getting a reward.<br/>
* **Policy**:- A strategy that the agent uses to identify which action it will perform next using only the current state.Its sort of a function or mapping.Usually probabilistic(converted from vectors using softmax function)in nature to allow the agent to perform stochastic actions(fancy word for exploring😁). It is represented as pie(a|s).<br/>
* **Return**:- Sum of all future rewards.<br/>
* **Spaces**:- Set of all posiible states/actions is called a/an State/Action Space.<br/>
* **State-Value Function**:- Conditioned that we arrive on a particular state(current state), it is the expected value to the return.<br/>
* **Action-Value Function**:- Conditioned that we arrive on a particular state s after performing an action a, it is the expected value of the return.In the Bellman equation equation, we can remove the pie(a|s) since a is given.<br/>
* **Bellman Equation**:- The mathematical equation, the solution for which solves the problem of our MDP.We possibly know the probability distribution of policies and the state-transitions in the Bellman equation so, it just boils down to a linear equation. <br/>
* **Optimal Policy**:- The policy that maximises the value function(for all states in the state space). It is denoted by V*(s) and by taking its argmax we can find the best policy pie*. Also, V*(s)=max(over all actions in the action space)Q*(s|a). Taking argmax of Q* gives the best action given any state.<br/> 
* **Discout Factor**:- For an Infinite Horizon MDP(or otherwise also), the further you go into the future the harder it is to predict, therefore we care about maximizing our rewards now.(gamma is a hyperparameter close to 1 for e.g:-0.99). Using this we can define the return recursively as G(t)=R(t+1)+gamma*G(t+1).<br/>
* #When the state encapsulates the complete information about the environment then we use deterministic rewards and policies. Other we represent them as probabilties to account for the loss of info for e.g:- We cant deterministically predict the next move by another chess player.<br/>
* #Finding the value function for a given policy is called the **Prediction Problem**.This is one type of problem in RL, the other being the **Control Problem** in which we have to find the optimal policy pie which yields the maximum value function(In this project, this is the problem that we would be solving).<br/>
**Now I will elaborate various methods/algorithms to solve the RL Control Problem:-**<br/>
* **Naive Approach**:-Exhaustively loop through all policies and return the one that yields the best State-Value function.(This has exponential time complexity as it will require |S|^^|A| iterations)<br/>
* **Monte Carlo Sampling**:-We can sample many returns to estimate the value function of each state.These samples can come from an episode because even if we use the same policy in the same environment, we will get different returns because both the policy and environment are probabilistic.Since, Q has more values than V, we need more samples to get a better estimate and thus this requires more time(Nested loops) so, instead of running through multiple episodes,we only run through one episode and then use the combination of the states,actions and policies.But, this does not give us a good estimate, so we write the next sample mean(estimated values) as a recursive relation which leads to an expression for Gradient Descent.Also, since newer samples matter more we use a constant learning rate leading to an exponentially decaying average.<br/> 
