## Project Overview

Nintendo created and distributed Super Mario Bros in the 1980s, and it is a well-known video game. It is a classic game title that has endured the test of time and requires no explanation. Using the Nintendo Entertainment System (NES) python emulator, the gaming environment was extracted from the OpenAI Gym. In this project, we use the PyTorch library to create the Reinforcement Learning method using the Deep Double Q-Network (DDQN) algorithms. We demonstrate how the recently developed Double Q learning (DQN) technique, which combines Q-learning with a deep neural network, may be utilised to create an agent that assists in completing levels in Super Mario Bros. The goal of Double Q-learning is to decrease over estimations by breaking down the target’s maximum operation into action selection and action assessment. The algorithm utilises the target network to estimate the value of the greedy policy based on the online network.

## Methodology
### Initializing the mario environment
Here we use the open ai gym library to create the super mario bro environment in which we then train our agent to make it learn and come up with optimal policy using the Double Deep Q learning (DDQL) method. once we have created the environment we then apply preprocessing to our environment so that the processing for our model becomes computationally less expensive. There are several steps adopted while pre processing the environment 
- Skipping the consecutive frames in the game because they dont vary much, we can set the parameter to skip knumber of intermediate frames. which doesnt make a much difference because we wont be loosing much information about the environment. we take the cummilative reward at the end of the nth frame over each skipped frame. 
- Combining multiple consecutive frames in the environment to get a single frame by using which we can determine the direction in which mario is moving, landing, jumping or running. 
- Converting each rgb frame to gray scale, and then the gray scale image is downsampled int a square image which makes further computations computationally less expensive. 
- Original mario consists of an action space 256 discrete actions, however to just prove the concept we restricted the action space to 7 discrete actions which is enough and sufficient for our agent to make mario complete the desired level we are training on.

### Creating the agent
The agent which we are training should be able to do the following mentioned things
- The agent should take the most optimal action policy based on the current state of the environment which when used should result in maximizing the reward the agent obtains. 
- Agent should be able to update the action policy by remmbering the past actions it performed. which can be implemented using caching. 
- The agent should be able to update to a new and better action policy everytime.

First the agent which we create can choose to perform the most optimal action (exploiting) or a random action (exploring). we perform exploiting using DDQN algorithm which helps us obtain the most optimal action our agent can perform in any given state. 

Each time when the action is performed by the agent the experience is stored in the memory using cache fucntion. Current state, action performed, reward from the action, the next state everything comes under experience of the agent. Then the experience from the memory is randomly sampled as batches which is then used for short term replay of the game.

### Learning
Double DQN Algorithm is used to learn the policy, the idea of Double Q-learning is to reduce overestimations by decomposing the max operation in the target into action selection and action evaluation. The algorithm evaluates the greedy policy according to the online network and uses the target network to estimate its value. The weights of the second network contain the weights of the target network for the evaluation of the current greedy policy. The update to the target network stays unchanged from DQN, and remains a periodic copy of the online network.

In normal Q-learning and DQN, the max operator selects and evaluates actions using the same values. As a result, selecting overestimated values is more likely, resulting in overoptimistic value predictions. To avoid this, we can separate the selection and evaluation processes. Double Q-learning is based on this concept. Two value functions are learned in the original Double Q-learning technique by randomly allocating each experience to update one of the two value functions, resulting in two sets of weights, and 0. One set of weights is used to decide the greedy policy and the other set is used to calculate its value for each update. We may first unravel the selection and assessment in Q-learning and rewrite it for a target.

![image](https://user-images.githubusercontent.com/53213766/174394281-8e546048-8ef5-4c72-a119-961ee60d4f77.png)

It's worth noting that the action selection in the argmax is still based on the online weights t. This indicates that, just like in Q learning, we're still predicting the greedy policy's value based on current values as described by t. However, to objectively evaluate the value of this strategy, we employ the second set of weights θ0. By reversing the roles of and θ0, the second set of weights can be updated symmetrically.

### Experimentation Results

Training Mario for 10 episodes Episode 10 score = 53, average score = 39.1
Training Mario for another 100 episodes Episode 100, score = 53, average score = 59.96
Testing Mario and gathering video of his performance over 2000 episodes Episode 2000 score = 392, average score = 392.0

### Conclusion
In this project, during the due course of our research we have come across multiple topic related research papers which talked about the game theory and most importantly Q learning, and also about the novel method of deep Q learning and DQN - deep Q network. This project was built on the motivation of making an RL agent which could train itself after multiple epochs based on Reinforcement learning and the concept of Double Deep Q learning, which enables this Mario playing RL agent to dodge obstacles and also gather points within the game with a very good coded reward process. Also miscellaneously, we have implemented the usage of OpenAI gym and nvidia system for the successful In completion of this project. In conclusion, this project is an extension of the usage of Deep Q learning algorithm and it’s related theories.
