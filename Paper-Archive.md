---
layout: page
title: "Paper Archive"
---

A reading list of papers I found or may find interesting. I've summarized the papers I've read or skimmed to a somewhat good understanding understanding.

## In progress

* [AlphaZero](https://science.sciencemag.org/content/362/6419/1140.full?ijkey=XGd77kI6W4rSc&keytype=ref&siteid=sci)

* [AlphaGo Zero](https://www.nature.com/articles/nature24270.epdf?author_access_token=VJXbVjaSHxFoctQQ4p2k4tRgN0jAjWel9jnR3ZoTv0PVW4gB86EEpGqTRDtpIz-2rmo8-KG06gqVobU5NSCFeHILHcVFUeMsbvwS-lxjqQGg98faovwjxeTUgZAUMnRQ)

* [AlphaGo](https://storage.googleapis.com/deepmind-media/alphago/AlphaGoNaturePaper.pdf)

* [Pointer Networks](https://arxiv.org/pdf/1506.03134.pdf)

* [General Game AI Reinforcement Learning](https://arxiv.org/pdf/1806.02448.pdf)

* [Hanabi](https://arxiv.org/pdf/1902.00506v1.pdf)

* [Curiosity - Rewardless Exploration](https://pathak22.github.io/noreward-rl/)

* [Apprenticeship Learning](https://ai.stanford.edu/~ang/papers/icml04-apprentice.pdf)

* [Relational Reasoning via Neural Networks](https://arxiv.org/pdf/1706.01427.pdf)

* [NLP vs. Protein Sequences?!](https://www.biorxiv.org/content/10.1101/622803v1)

## Archive

[Learning Abstractions by Transferring Abstract Policies to Grounded State Spaces (2018)](https://www.aaai.org/ocs/index.php/SSS/SSS18/paper/viewFile/17551/15537)  
Unlike humans, robots are unable to abstract important details of any 2D map to navigate the 3D world and vice versa. It may be possible to abstract important aspects of the navigation policy to an abstract policy that can deal with any new map using any of the following or more: isometric path (forward 5 blocks, turn right, etc.), landmarks (including street names), topological path (convert whole map to nodes), and even NLP (voiced instruction abstraction). With this, we could train AI through supervised learning easier as the instructions are abstracted and the bulk of the state space is up to the agent to discover.

[High-level Reinforcement Learning in Strategy Games (2010)](https://pdfs.semanticscholar.org/9f9c/0f114b0c4d9b13ec048507a178fe9b3da4ae.pdf)  
Hard-coding AI into games should be a thing of the past now that reinforcement learning techniques have proven to be very efficient, often more powerful, and fairly easy to use. Trained minimally (100 episodes) in the complex strategy game of Civilization IV, agents using techniques such as Q-learning and Dyna-Q have done well against low-level, fixed-policy opponents even with state, action, and reward simplifications. We are trading time used to hard-code strategy into an AI with compute-time of having the AI train itself in varying levels of power based on complexity of the algorithm and training time.

[The Art of Drafting: A Team-Oriented Hero Recommendation System for Multiplayer Online Battle Arena Games (2018)](https://arxiv.org/pdf/1806.10130.pdf)  
Drafting in MOBA games can be considered a combinatorial game of its own with both sides trying to maximize win chances by out-drafting the other team through counter-picks and team synergy. UCT Monte Carlo Tree Search converges to a relative optimum (the minimax optimum) in polynomial time based on pre-acquired winning percentages learned by neural networks for both regular drafting and ban-enabled drafting. The research shows how well MCTS does without the need for exhaustive search as well as the capability for generality should the researchers wish to incorporate further parameters (player perferences, etc.).