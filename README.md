# Trading_Bot_using_Reinforcement_learning
This repository contains the python code for the implementation of a trading bot using Reinforcement Learning Algorithms.<br/>
*A **Reinforcement learning** problem is mathematically modelled as a **Markov Decision Process**(which follows the Markov Assumption i.e the next state depends only on the immediate previous state),the Main elements in which include: 1)Agent 2)Environment.<br/>*
Apart from these there are several other elements which help us to describe the interaction between agent and environment namely:-<br/> 
&ensp; 1)Episode <br/> 
&ensp; 2)State <br/>
&ensp; 3)Action <br/>
&ensp; 4)Reward <br/>
&ensp; 5)Return <br/>
&ensp; 6)Q function <br/>
&ensp; 7)Policy etc. <br/>
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
* **Bellman Equation**:- A mathematical equation, the solution for which solves the prediction problem of our MDP.We possibly know the probability distribution of policies and the state-transitions in the Bellman equation so, it just boils down to a linear equation. <br/>
* **Optimal Policy**:- The policy that maximises the value function(for all states in the state space). It is denoted by V*(s) and by taking its argmax we can find the best policy pie*. Also, V*(s)=max(over all actions in the action space)Q*(s|a). Taking argmax of Q* gives the best action given any state.<br/> 
* **Discout Factor**:- For an Infinite Horizon MDP(or otherwise also), the further you go into the future the harder it is to predict, therefore we care about maximizing our rewards now.(gamma is a hyperparameter close to 1 for e.g:-0.99). Using this we can define the return recursively as G(t)=R(t+1)+gamma*G(t+1).<br/>
* #When the state encapsulates the complete information about the environment then we use deterministic rewards and policies. Other we represent them as probabilties to account for the loss of info for e.g:- We cant deterministically predict the next move by another chess player.<br/>
* #Finding the value function for a given policy is called the **Prediction Problem**.This is one type of problem in RL, the other being the **Control Problem** in which we have to find the optimal policy pie which yields the maximum value function(In this project, this is the problem that we would be solving).<br/><br/>
## **Various methods/algorithms to solve the RL Prediction/Control Problem:-**
* **Naive Approach**:-Exhaustively loop through all policies and return the one that yields the best State-Value function.(This has exponential time complexity as it will require |S|^^|A| iterations)<br/>
* **Monte Carlo Sampling**:-We can sample many returns to estimate the value function of each state.These samples can come from an episode because even if we use the same policy in the same environment, we will get different returns because both the policy and environment are probabilistic.Since, Q has more values than V, we need more samples to get a better estimate and thus this requires more time(Nested loops) so, instead of running through multiple episodes,we only run through one episode and then use the combination of the states,actions and policies.But, this does not give us a good estimate, so we write the next sample mean(estimated values) as a recursive relation which leads to an expression for Gradient Descent.Also, since newer samples matter more we use a constant learning rate leading to an exponentially decaying average.<br/> 
* **Explore-Exploit Dilemma**:- We want to exploit the Action-Value function(get the best possible value) and at the same time get more data so that our estimate is more accurate(let our agent explore).So, instead of just always performing the action specified by the policy we will sample a random number and if it is less than an arbitary number(epsilon) then we will choose a random action from the action space.Otherwise, will choose the action specified by the greedy policy(which is greedy with respect to Q).This method is called the **Epsilon-Greedy**.<br/>
* **Limitations of Monte Carlo** :-In order to calculate returns, we must wait until the episode is over.This follows from the definition of return(Sum of future rewards until the episode is over).What if we have very long episodes or an environment with no terminal state.In these cases, Monty Carlo is not an option.<br/>
* **Temporal-Difference Methods**:-Temporal Difference is an approximation to the MC.It is an approximation to an approximation.(I accepted defeat on reading/learning this and had to repeat the entire course in order to get the hang of why/how we reached here🤯🤕).Now, instead of using the full return, we aere going to estimate the return.We collect the next reward and instead of collecting any future rewwards,we will simply guess that they will be close to V(s').Mathematically this become:- G=r+G' is approximately equal to r+V(s').{V(s') is the expected value of G'}.So, we wait only one step for updating our model.This the **Bootstrapped Estimate** of the return.This method is known as TD.It is used to solve the predicition problem.<br/>
* **Q-Learning**:- This Algorithm is used to solve the control problem.We use the epsilon greedy method to determine which action we are going to take next and then execute this action in the environment.Next, we update our Q-value using gradient descent where the target is estimated(in supervised learning we are given the target) by performing the greedy action and taking the max over Q given the state s'.{Yes Yes ik, gradient descent is a part of supervised learning and so in essence,an RL problem becomes a supervised learning problem without the targets being specified}<br/>
* **ADVANTAGES**:- 1)We dont have to wait until we perform the next action to update Q. 2)Although, we can explore freely,the algorithm will always greedily update the Q-table.<br/>
* **DEEP Q-LEARNING**:-In Q-learning, we try to obtain the optimal Action-Value function Q and the optimal policy pie.If the states and actions are discrete we can use a Q-table for this.In case of infinite state or action spaces, this is not an option.Therefore, we are forced to use approcimation methods. One assumption that we make is that,the state space can be infinite but, the action space is discrete.The state is thus stored in a vector and the Q-value is approximated as linear regressions(Q(s,a0)=w0^T*s+b0).So, now we have to update the weight matrix and bias vector instead of directly updating Q or V.But, it is not necessary that the Q-value is linearly dependent on s and here is where neural networks come into play!!But, there is another problem, we cant just use any learning rate,any optimizer, any architecture and so on.Also, we are using TD methods which are approximation and thus, inherently unstable. Everything, is not actual,it is an approximation.So, instead of using Stochastic gradient descent(one sample at a time), we will use batch gradient descent(which uses multiple samples at a time)in order to stabilize the gradient.So, we will use the experience replay buffer (which maintains the set of all transitions from which we sample a batch of transitions)approach to Deep Q-learning.<br/>
* We dont like correlated samples when we are doing gradient descent but, in RL the data is very correlated we are going from one state to the next in an MDP.So, we shuffle the data on each epoch.<br/><br/>
### **CODE DESCRIPTION**
* The Environment(Stock Market simulation) mimics the OpenAI GYM API.
* The next elements are inspired from the research paper "Practical Deep Reinforcement Learning Approach for Stock Trading".We will be using 3 companies namely:- 1)Apple 2)Motorola 3)Starbucks.
* **STATE**:-<br/>
&ensp; *How many shares of each stock we own.<br/>
&ensp; *Current Price of each stock.<br/>
&ensp; *How much remaining cash we have left.<br/>
* **ACTION**:-<br/>
&ensp; *BUY/SELL/HOLD.<br/>
&ensp; ***SIMPLIFICATIONS**:-We ignore any transition costs.We will sell all shares of the stock that we own.We will buy as many stocks as we can.We will sell before buying to obtain more in-hand cash.<br/>
* **REWARD**:-<br/>
&ensp; *Change in portfolio value from one state to another.Total price of shares owned plus the in-hand cash. 
