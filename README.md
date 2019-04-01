# DeepRL_DDPG
Single Agent DDPG (Deep Deterministic Policy Gradient) Implementation

In this repository it's shown the usage of a Deep Reinforcement Tecnique called DDPG or Deep Deterministic Policy Gradient, which uses the concepts of Reinforcement Learning applied in a controlled enviroment. Using a Deep Neural Network as a Function Approximator to map state to action pairs, in order to decide how an agent has to act given it's current state and the discounted cummulative reward. Additionally, this tecnique is able to manage any enviroment that has a set of continuos actions, which makes it extremaly useful in real life applications.

## The Enviroment
The objective of the enviroment is to be used as a playground to train a single agent that is capable of following some continuously changing positions in space which are is target locations. The agent is a double-jointed arm that recieves a reward of +0.1 for each step that it's hand is in the goal location. Thus, the goal of the agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

The task is episodic, and in order to solve the environment, the agent must get an average score of +30 over 100 consecutive episodes.

## Setting Up the Enviroment
Follow the instructions below to explore the environment on your own machine! You will also learn how to use the Python API to control your agent.

### Step 1: Clone the DRLND Repository
Please follow the [instructions in the DRLND GitHub repository](https://github.com/udacity/deep-reinforcement-learning#dependencies) to set up your Python environment. These instructions can be found in README.md at the root of the repository. By following these instructions, you will install PyTorch, the ML-Agents toolkit, and a few more Python packages required to complete the project.

(For Windows users) The ML-Agents toolkit supports Windows 10. While it might be possible to run the ML-Agents toolkit using other versions of Windows, it has not been tested on other versions. Furthermore, the ML-Agents toolkit has not been tested on a Windows VM such as Bootcamp or Parallels.

If you are having troubles connecting to the enviroment's jupyter notebook kernel, remember to reinstall jupyter on that particular enviroment. If you are using Linux, use the next line of code on your terminal: ```conda install jupyter```

### Step 2: Download the Unity Environment
For this project, you will not need to install Unity - this is because there is an already built environment to work with, and you can download it from one of the links below. You need only select the environment that matches your operating system:

* Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip)
* Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip)
* Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86.zip)
* Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip)

Then, place the file in the ```p2_continuous-control/``` folder in the DRLND GitHub repository, and unzip (or decompress) the file.

(For Windows users) Check out [this link](https://support.microsoft.com/en-us/help/827218/how-to-determine-whether-a-computer-is-running-a-32-bit-version-or-64) if you need help with determining if your computer is running a 32-bit version or 64-bit version of the Windows operating system.

## Running the Agent
Once you have set up the enviroment, go to **5. Testing Agent After Learning** in Continuous_Control.ipynb, and run all the cells except the last one which closes the enviroment. If the path to your enviroment is different, just change it in the cell below **Loading Enviroment**. You will be able to see in the unity window how the agent is sticking to its target position, which is moving in a continuos manner, as the agent's own joints. If you want to see various episode runs, just rerun the times you want the cell below **Running Episode**
In the Case you want to train the agent from scratch, run all the cells from **4. It's Your Turn** section, and you'll be able to see the training process and the reward plot per 100 episodes. There you will save the weights learned, and the files can be used to test the agent thereafter.







