## Report

### The Enviroment
In this implementation i used a DDPG (Deep Deterministic Policy Gradient) method to solve the Continuos Control enviroment. 
The objective of the enviroment is to be used as a playground to train a single agent that is capable of following some continuously changing positions in space which are is target locations. The agent is a double-jointed arm that recieves a reward of +0.1 for each step that it's hand is in the goal location. Thus, the goal of the agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

The task is episodic, and in order to solve the environment, the agent must get an average score of +30 over 100 consecutive episodes.

### The Learning Algorithm
To solve the enviroment i used the Deep Deterministic Policy Gradient Algorithm (DDPG). This is an Actor- Critic method, that means that we have a neural network (The Actor) that interacts with the enviroment given the input states. The Actor for this method is deterministic, that means that we are not recieving a probability distribution over the actions, rather they are being approximated by the neural network directly. Afterwards, the actions approximated by the Actor are fed back as input to the Critic (Q(s, a), substitute the actor network for a), which is another neural network that approximates the action-value functions and its trying to maximize them to find the optimal policy. This is accomplished by expressing the output of the critic in terms of loss of the actor, i.e. loss(actor) = - output(critic). We backpropagate that loss to update the Actor Networks. 
Given that the learning is off-policy, we need a replay buffer to store experiences from the agent. Therefore as in the DQN algorithm we have a local and a target network as well, one that interacts with the enviroment and the other one that is being updated constantly.We have then 2 netowrks for the Actor and 2 Networks for the Critic. After a few steps, we make a soft update to the networks from the experiences stored away. Learning from the Critic is done with Q learning, where we are updating the Q values, from the predicted  next Q value from next state, times the discounting factor, plus the reward. Then, the loss of the critic, loss(critic) = F.mse_loss(Q_expected, Q_targets). Where Q_expected comes from the output of the local Critic Network, and Q_targets comes from the adjusted Q learning step. Finally we backpropagate that loss to update the Critic Networks. 

In summary, the algorithm has 2 important processes that work inside it. In the first one, the agent samples the enviroment by performing actions and stores away the different experience tuples in a replay memory. In the second one, the agent selects a random batch of experiences from the replay buffer and learns from it using a gradient descent step. Iterating over these 2 steps leads the agent to learn how to interact with the enviroment abstracting the optimal policy from the learned action value function.

### Neural Networks
The Actor Neural network is a 3 layer feed forward network with Tanh activation between layers and in the output layer aswell, given that the actions have to be sampled from a continous space of -1 to 1. The output of the actor network has the size of the enviroment action space, that is a vector of 4. 

The Critic Neural network is a 3 layer feed forward network with Relu activation between layers. In the first layer, the network is fed with the state of the enviroment; in the second layer, the output from the first layer is concatenated with the action recieved from the actor. Finally, the critic network output is a single value with the approximated value function given the actor's action .

Given that for this particular problem the input are not the raw pixels from the enviroment, rather the 33 states that contain the agents position, rotation, velocity, and angular velocities of the arm, there was not need for the implementation of a convolutional neural network.

### The Hyperparameters
Buffer Size = 300000
Batch Size = 512
Gamma = 0.99
Tau = 0.001
Actor Learning Rate = 0.0001
Critic Learning Rate = 0.001

The Actor and Critic networks were updated through the learning process, every 30 time steps if the memory buffer had at least the same ammount of experiences as the minimum batch size.

Number of Episodes = 1000
Max number of Steps per Episode = 1000

Also the Ornstein-Uhlenbeck process which adds noise to the actions selected by the Actor Nework, a normal distributions was used instead of a uniform distribution.

### Plot of Rewards per Episode
![Image of Reward PLot](/training_results/reward_plot_ddpg.png)
![Image of Training Process](/training_results/training_process_ddpg.png)

The Enviroment was solved around episode 500

### Ideas for Improving Agents Performance
One of the things that may be hindering performance is the random selection of experiences from the memory buffer. Why? because not every experience is the best experience that can be used to learn. There are some specific experiences that should be used more than others to improve learning in some aspects. Also, there are some experiences that are less common that others, and some of those may have valuable information that can not be neglected. So, if one could give a weight to each particular experience in a way that allows to take one particular experience more often than others, learning could be improved and could actually converge faster.
