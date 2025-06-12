# Optimizing NBA In-Game Decisions with Neural Networks and Deep Q-Learning

**Authors:** Will Nyman, Raul Sharma, Oren Abutbul  
**Code:** [GitHub Repository](https://github.com/raulsharma21/NBA-Actions/)

---

## Table of Contents

- [Background and Motivation](#background-and-motivation)
- [Data Acquisition and Preparation](#data-acquisition-and-preparation)
- [Design](#design)
- [Implementation](#implementation)
- [Results](#results)
- [Practical Applications](#practical-applications)
- [Limitations and Future Work](#limitations-and-future-work)
- [Setup Instructions](#setup-instructions)

---

## Background and Motivation

In professional basketball, real-time decisions—such as whether to shoot or pass—can determine the outcome of a game. While machine learning is used in the NBA for outcome prediction, team construction, and injury analysis, our project focuses on optimizing in-game shot selection using a two-stage learning framework:  
1. A neural network predicts shot success probability.  
2. A Deep Q-Learning agent uses this probability and game context to learn optimal actions (shoot, pass, move).

---

## Data Acquisition and Preparation

- **Source:** [nba_api](https://github.com/swar/nba_api)
- **Focus:** Stephen Curry's shots (2016-17 to 2023-24)
- **Feature Engineering:**
    - Encoded time, home/away, shot location, angle, and distance
    - One-hot encoding for shot zones
    - Feature selection via SKLearn

**Core Features:**
- Period (int)
- SHOT_ZONE_BASIC (string)
- SHOT_DISTANCE (double)
- LOC_X, LOC_Y (double)
- TIME_REMAINING (int)
- HOME (bool)
- ANGLE (double)
- SHOT_MADE_FLAG (bool)

---

## Design

- **Stage 1:** Neural network estimates shot probability from context.
- **Stage 2:** Deep Q-Network (DQN) uses shot probability and game state to learn optimal actions.
- **Action Space:** Shoot, Pass, Move
- **Reward Structure:** Rewards/penalties based on basketball intelligence and shot quality.

---

## Implementation

### Neural Network for Shot Probability

- **Framework:** TensorFlow/Keras
- **Architecture:** 3 hidden layers (128, 64, 32 units), dropout, sigmoid output
- **Training:** Adam optimizer, binary cross-entropy, 20 epochs, batch size 32
- **Metrics:** Accuracy, precision, recall, AUC

### Deep Q-Learning

- **Environment:** Custom basketball simulation
- **State:** Normalized court position, game context, shot probability, home/away
- **Actions:** Shoot (0), Pass (1), Move (2)
- **Rewards:** Based on shot outcome, passing up low/high probability shots, movement improvement
- **Learning:** Experience replay, epsilon-greedy policy

---

## Results

- **Neural Network Accuracy:** 54%–68% (reflects basketball shot variability)
- **DQN Training:** Rewards stabilized, agent learned to avoid poor shots
- **Final Policy:**  
    - Shooting: 9.7%  
    - Passing: 29.9%  
    - Moving: 60.4%
- **Behavior:** Selective shooting, ball movement, spatial awareness

---

## Practical Applications

- Shot quality assessment for coaches
- Player development feedback
- Game preparation and simulation
- Potential for real-time decision support

---

## Limitations and Future Work

- Does not model teammates or defenders
- Reward structure requires manual tuning
- Future: Multi-agent environments, defensive data, team dynamics

---

## Setup Instructions

1. **Clone the repository:**
     ```bash
     git clone https://github.com/raulsharma21/NBA-Actions.git
     cd NBA-Actions
     ```

2. **Create and activate a virtual environment:**
     ```bash
     python3 -m venv venv
     source venv/bin/activate  # On Windows: venv\Scripts\activate
     ```

3. **Install dependencies:**
     ```bash
     pip install -r requirements.txt
     ```

4. **Run the code:**  
     Use the python notebooks in the repository for data preparation and model training.

---

**For questions or contributions, please open an issue or pull request.**
