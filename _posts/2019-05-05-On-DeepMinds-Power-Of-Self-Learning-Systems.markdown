---
layout: post
title:  "On DeepMind's Power of Self-Learning Systems"
date:   2019-05-05 21:32:00 -0500
categories:
---

I recently viewed DeepMind's talk describing their previous successes with AlphaGo, AlphaGoZero, and AlphaStar. In the lecture, DeepMind described not only their successes, but the importance of their research in many applicable fields. As you may know, DeepMind was and still is one of my primary points of inspiration in my journey in AI/vision. I highly recommend anyone interested in AI to watch it:

<iframe width="560" height="315" src="https://www.youtube.com/embed/3N9phq_yZP0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>









## **My Summary**
DeepMind started by attacking Atari's breakout. Not much was said about the game but it seemed like a relatively easy problem to tackle. Their first huge success was in Go. DeepMind used two systems: AlphaGo and AlphaGoZero. AlphaGo learned by initially watching other people play and attempting to mimic their moves. From mimicking, the AI finds ways to counter the player strategies and goes on to play itself until it becomes the best it can be. AlphaGoZero learned completely by itself; no spectator learning was necessary. These two AI's went on to beat the human champions of Go. From these achievements came AlphaZero, which was built for chess, but may potentially be applied to any two-player strategy game. AlphaZero dominated the chess world as its predecessor dominated the Go world. From these came AlphaStar which was designed for Starcraft II, a game of imperfect information. Like the others, AlphaStar is ranked above the grandmasters of Starcraft II. Even though DeepMind tackled strategy games, their research can definitely be applied to real life, particularly in the protein folding problem.

## **Why I'm Interested**
The lecture really emphasized why I was originally inspired by DeepMind and why I continue to do the projects I'm undertaking. My field of interest involves providing an AI an environment and having it learn in that environment. Vision allows the AI to extract current game-states or environment-state for analysis in the backend. Learning allows the AI to attempt to solve a problem. As a result, an answer may be produced based on the AI's understanding of the world it is in. DeepMind did exactly this in AlphaStar. AlphaStar was able to extract information from the map about where the enemy units are, what the enemy is building, what AlphaStar had at ready, etc. It could then predict its probability of winning and take the steps necessary to win the game.

I'm even more invested in what we as humans can learn from AI, something that DeepMind also emphasizes (this was the first time I heard that they share this philosophy). For example, humans have always known that 1. E4 is the best opening move for chess. We know that by statistics, activity of openings, etc. However, AlphaZero showed us that 1. E4 is best because of the potential to play E5 later in the game. A white pawn on E5 encroaches deeply on black's space, as there is usually a knight on F6 and king-side castle. I myself am not an amazing chess player, but it is fascinating nonetheless.

DeepMind continually emphasized the importance of learning something from their AI, like learning new strategies that spark new metas in Starcraft II. This brings me back to my interest in a Tetris AI. Why am I doing it? Because I primarily want to learn whether a flexible T-spin playstyle is better than a quick back-to-back Tetris playstyle or any of the combo playstyles.

## **Random Notes**
Expert systems are systems where almost every rule and exception is hard-coded into an AI. This method attempts to create the strongest brute-force AI possible. Learning systems attempt to learn the most optimal way to play with limited or no rules and exceptions. By using well-optimized learning systems, you cut down massively on necessary compute power. Of course, I still believe learning systems can be flawed as they have somewhat human-like behavior and, as such, potential for blunder.

Someone mentioned that, although AlphaStar played below the average grandmaster APM, its peak during battles far exceeded human-like APM. Particularly in game 4 vs MaNa, the human could not keep up because AlphaStar set up a three-pronged attack where it controlled every flank perfectly and quickly. You can see it here: [DeepMind Starcraft II Demonstration](https://youtu.be/cUTMhmVh1qs?t=6158) (time 1:42:38). Takeaway: if going for artificial human-like intelligence, keep in mind the limits of human ability and seek to win through intelligence and clever strategies.

DeepMind mentioned that AlphaZero seemed to evolve some sort of creativity - an ability to come up with a novel move that no one had thought of yet. I really like this about learning systems. They have so much creative space since they are learning from scratch that they are bound to find new and enriching ideas.

We are just at the beginning of artificial intelligence and learning. There is so much more to tackle in the coming decades and I'm very glad to soon join in on the research. I hope to one day do cool things like DeepMind (and OpenAI) does.
