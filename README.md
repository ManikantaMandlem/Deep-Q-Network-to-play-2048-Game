# Deep-Q-Network-to-play-2048-Game

This repo contains different versions of DQN agents that can be trained to play 2048 game. Below are some details for different versions.

Please refer to report for more information on training and results

## Testing on Cartpole:
Before moving forward to train the agent on 2048, we wanted to check the correctness of the implementation by running the code on the OpenAI gym Cartpole v1 environment. Details of this implementation can be found in: DRL_Final_Project_cartpole_test.ipynb

## Strategy 1:
Reward is calculated as a function of the configuration of the game state. This strategy is inspired by the basic strategy of a human game-play which is to maintain the largest value tile on one of the corners and other large values in the same row or column and make sure to maintain such configuration while clubbing new numbers while playing the game. This way there is less chance to end the game with many small numbers spreaded across the grid.
To make the agent learn this kind of play, we rewarded the agent with the value of the tile present in the bottom left corner and value/2 of the number next to it and value/4 of the second next number and finally value/8 of the bottom right tile. This way we believe that we are encouraging the agent to put high value tiles in the bottom row with highest values towards the left. We ran this script on Quest HPC with 700 episodes, gamma = 0.95, batch_size = 512 and learning rate = 0.0001.
The agent was able to score two 128 tiles in a lot of episodes and also scored 256 in a significant number of episodes. The detailed output of each episode can be found in imp1.txt file. Details of this implementation can be found in: DRL_Final_Project_strategy_1.ipynb

## Strategy 2:
We wanted to see how the agent would perform if the reward it received is the sum of the numbers present on the grid. With the assumption that the agent would be able to score high while trying to maximize the sum of the numbers on the board, we implemented this strategy. We ran the script with 700 episodes of training. Below is a graph depicting the number of moves made by the agent in each episode.
In this strategy we observed that the agent is able to score 256 in lesser time as compared to when training in the previous strategy. The detailed output of each episode can be found in the imp2.txt file. Details of this implementation can be found in: DRL_Final_Project_strategy_2.ipynb

## Strategy 3:
In 2048 a single bad move can potentially ruin the entire setup of the game and can end the game rather quickly. Given this, we thought that an epsilon-greedy policy might not be a good one to learn 2048. While the agent explores, one random move can result in a bad one and end the game quickly. So we tried out a different probabilistic policy with inspiration from the research by Jonathan et. al., [1]. Instead of using the output of the neural network as Q_Values directly, we calculated the softmax of the values and considered the resulting numbers as probabilities with which the corresponding action should be taken. This probabilistic policy is inherently explorative as the selected action need not necessarily be the optimal action all the time. Apparently after training for 700 episodes we could not see any significant learning by the agent. Details of this implementation can be found in: DRL_Final_Project_strategy_3.ipynb

## Training on Tiny-2048 game:
We have trained an agent to play a tiny-2048 game which is a 2x2 grid instead of 4x4 grid. Though the training process did not take much time, the agent was able to achieve the highest tile (of 16) many times. Details of this implementation can be found in: DRL_Final_Project_tiny_2048.ipynb
