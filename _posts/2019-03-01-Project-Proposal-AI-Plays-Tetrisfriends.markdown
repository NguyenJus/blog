---
layout: post
title:  "Project Proposal: AI Plays TetrisFriends"
date:   2019-03-01 18:09:00 -0500
categories:
---

### Project name: AI Plays TetrisFriends

This four-part project will attempt to train an AI to play Tetris on [TetrisFriends.com](Tetrisfriends.com). It will be able to pull data non-invasively from the website using screen capture and make calculations accordingly. It will succeed in playing Tetris, and perhaps optimizing its score. The method of training chosen is reinforcement learning.










## Background
Tetris is, in essence, an optimization game. The game board is a 10 x 20 grid of blocks. A player receives one of seven different pieces consisting of four blocks at a time and must place them in a way that whole rows are filled. The pieces and their respective names are as follows:

![screenshot](https://qph.fs.quoracdn.net/main-qimg-356e2b21c801381db2890dab49a9ea88)

*Fig 1: Playable Tetris pieces [Tetrominoes] [source](https://www.quora.com/What-are-the-different-blocks-in-Tetris-called-Is-there-a-specific-name-for-each-block)*

When a whole row is filled, the row disappears and all rows above it are moved down. A player loses when they "top-off" - when a tetromino exceeds the 20-block height restriction. The goal of the game is to clear as many rows, "lines," as quickly as possible.

In general, the player receives a better score if more lines are cleared at once or are cleared consecutively. The scoring system will be more thoroughly explained in the actual project. Exceptions are special clears called t-spins and perfect clears, which score high amounts of points relative to lines cleared. It will be interesting to see whether the AI can find these methods.

The optimization comes naturally with reinforcement learning. The AI will score points whenever it places tetrominos as well as clear lines. The more points it receives, the more likely it will try to replicate that clear.

### Why?
This project will touch upon several different problems which may be solved with mini-projects. Its primary purpose is to learn about how to solve problems using various technologies. Tetris will not be recreated in a private environment because I want the AI to extract information directly from the screen.

Besides this, I also wanted to see whether the AI can calculate the most optimal strategies for clearing lines. There are many methods to play: 2-wide combo, 3-wide combo, 4-wide combo, back-to-back tetris, t-spin, perfect clear, middle combo variants, and more. If the AI can find the best method to score, it will be good to utilize that method in online play.


## Method
There will be four smaller projects which culminate to this project, all of which will utilize technologies and code relevant to the main project. These are: an osu!mania bot, a sudoku extractor, a general reinforcement learning program, and finally, AI Plays TetrisFriends.

### Part 1: Osu!ManiaBOT
Osu!Mania, part of [Osu!](https://osu.ppy.sh/home), is a game like Stepmania or Dance Dance Revolution. Using a [reskin](https://osu.ppy.sh/community/forums/topics/512453), I can recreate the arrow mechanisms used in Stepmania and Dance Dance Revolution. The goal of the game is to press the corresponding arrow key when it reaches the top of the screen.

![screenshot](https://i.ppy.sh/ec560eab801b2fab6d8b816956988ed3bc00252a/68747470733a2f2f7075752e73682f7a3454756d2e6a7067)
*Figure 2: Osu!Mania reskin [source](https://osu.ppy.sh/community/forums/topics/512453)*

Therefore, in order to succeed, a program must be able to detect whether an arrow is at a certain point and press the matching key. The pixel detection and key inputs will also be used in the main project.

### Part 2: Sudoku Extractor
Sudoku is a puzzle game played on a 9x9 grid where the numbers 1-9 may only be placed once per row, column, and 3x3 box.

![screenshot](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/Sudoku_Puzzle_by_L2G-20050714_standardized_layout.svg/250px-Sudoku_Puzzle_by_L2G-20050714_standardized_layout.svg.png)

*Figure 3: Typical Sudoku Puzzle [source](https://en.wikipedia.org/wiki/Sudoku)*

In order to extract the sudoku from various web pages, the program must be able to detect whether there is a grid present and pull numbers from the grid. The number recognition likely needs to be trained using a neural network. In the main project, the capacity to detect a grid will be used to find the environment of the Tetris game, and the number recognition will be used to pull the score for calculations.

### Part 3: Reinforcement Learning
A model of reinforcement learning on a simple game will be created in order to learn about the training method. Currently, no game has been selected for the training. I anticipate using TensorFlow for the project. This relates to the main project as the Tetris AI will also be using reinforcement learning.

### Part 4: AI Plays TetrisFriends
The final part of the project will be to combine everything into one project. The AI will be able to find the Tetris grid, pull pixel data from its 200 grid blocks, find its score and calculate accordingly, and just play the game. It will be trained in Tetris Marathon, a mode that ends after 15 levels.

![screenshot](https://raw.githubusercontent.com/NguyenJus/blog/gh-pages/assets/img/TetrisMarathon.png)

*Figure 4: Tetris Marathon Play Space [source](https://www.tetrisfriends.com/games/Marathon/game.php)*


## Further Research
Every part of this project has the potential to do more than it is intended to do. As I find inspiration or new features, I may revisit the projects and add to them.

Hopefully everything works out okay. I'm excited to start this journey and to report on it!
