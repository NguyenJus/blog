---
layout: post
title: "Paper Archive"
---

In no particular order (yet), I've summarized various papers that I've read or skimmed to a good understanding. A * denotes that I may need to recheck the summary.

*[Learning Abstractions by Transferring Abstract Policies to Grounded State Spaces (2018)](https://www.aaai.org/ocs/index.php/SSS/SSS18/paper/viewFile/17551/15537)  
Unlike humans, robots are unable to abstract important details of any 2D map to navigate the 3D world and vice versa. It may be possible to abstract important aspects of the navigation policy to an abstract policy that can deal with any new map using any of the following or more: isometric path (forward 5 blocks, turn right, etc.), landmarks (including street names), topological path (convert whole map to nodes), and even NLP (voiced instruction abstraction). This research would suggest that we can train AI through supervised learning easier as the instructions are abstracted and the bulk of the state space is up to the agent to discover.
