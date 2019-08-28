---
layout: post
title:  "Enchanting Simulation - MapleStory2"
date:   2019-08-15 11:38:01 -0500
categories:
---

Over a month ago, I was rushing to get entry into Blackshard Nexus, the final raid in [MapleStory2](http://maplestory2.nexon.net/en) at the time. The raid required a specific level of upgraded gear that needed to be acquired in a small amount of time. Although upgrade systems are all luck, we can manipulate the expected probabilities to our favor and have, overall, a better chance at making cuts. To do this, I simulated the game's enchantment system and threw millions of runs at it! I can't say that the outcome helped me exactly since it's all an RNG system, but it certainly helped me pick a method to enchant my items with. In the end, I made it in and cleared the raid on my first week! (my username is hidden)

<img src="https://nguyenjus.github.io/blog/assets/img/EnchantSuccess2.jpg">







## Source Code

[Github](https://github.com/NguyenJus/MS2-Enchant-Simulation)

## Introduction

When we play MMORPGs, there is always some type of item upgrading system which heavily relies on luck. These upgrades typically have a hard cap on maximum amount of upgrades (+10, +15, etc.). Sometimes, the item may break so we must come up with a way to minimize our losses while maximizing our output. Fortunately, more recent games do away with this breaking system, so we only have to worry about maximizing our output while minimizing our costs. Each game's system may vary slightly. Some favor the user. Others favor the company profits. If we can minimize expected costs, we can pray and hit upgrade thresholds in a reasonable amount of time and resources.

### The System in MS2

MS2 features upgrades from +0 to +15 incrementing by one on success. The higher the upgrade, the lower the success rate: 

```
OPHELIA = [1, 1, 1, 0.95, 0.90, 0.80, 0.70, 0.60, 0.50, 0.40, 0.30, 0.20, 0.15, 0.10, 0.05]
```

There are two systems to upgrade your items. Ophelia is luck-based with the probabilities given above. Peachy is guaranteed but costs more resources on average. The user may interweave between either system, leading to some creative methods. 

The main limiting resource is the weapon. The amount of weapons required to attempt an upgrade are as follows:

```
WEAPON_COST = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 2, 2, 3, 3, 4]
```

#### Failstacks

Each time the user fails, they gain one failstack plus one per weapon used. Each failstack provides +1% success rate when used. These failstacks are accumulated over time and are one-time use. 

#### Extra Resources 

The user can choose to add additional resources of the same type (using extra weapons to upgrade a weapon, etc.) for an increase in success rate up to a maximum of 30%. The increase varies based on the current upgrade level:

```
OPHELIA_EXTRA_WEAPONS = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0.07, 0.05, 0.04, 0.02]
```

Note this only starts taking effect +11. 

## Simulating

The goal of the upgrade was to reach +14 using as few weapons as possible. The system can also be used to find expected outcomes for any other enchantment level. Using the guaranteed Peachy method, the total cost is 55 weapons. How can we best beat this manipulating failstacks and extra resources?

I wrote a few cases and tested them all on 100000 simulations. Here is the best one for example: 

```
average = 0
    for i in range(100000):
        w = Weapon()
        while w.enchant < TARGET:
            if w.enchant == 13:
                w.enchant_with_ophelia(0, w.failstacks)
            else:
                w.enchant_with_ophelia(0, 0)
        average = (average*i + w.weapon_cost)/(i+1)
```

Prior to this, I did some calculations and found the above to be the best method. The simulation agreed. The method was to always use Ophelia system without any failstacks or extra resources. When you reach +13, throw all your failstacks into one big enchant without any extra resources. Here are the results:

```
    # These methods assume 0 failstack, 0 weapon usage before +13
    # 51.2364: 0 weps, failstack dump at 13 + 0 extra weps
    # 51.2975: 0 weps, failstack dump at 13 + 1 extra wep
    # 51.4172: 0 weps, failstack dump at 13 + 2 extra weps
    # 51.5569: 0 weps, failstack dump at 13 + 3 extra weps
    # 51.7857: 0 weps, failstack dump at 13 + 4 extra weps
    # 52.0763: 0 weps, failstack dump at 13 + 5 extra weps
    
    # This method simply throws all failstacks as they are acquired
    # 54.1322: 0 weps, dump all failstacks
```

Most of the other experimental methods I tried were worse than taking the guaranteed route. As you can see, the expected outcome of the best method saved 3.7 weapons, which is a 6.8% decrease. Of course, there are more complicated methods, specifically for +15 since the guaranteed method required resources jumps from 55 to 87. Those methods attempt to manage failstacks properly at various thresholds (70, 95, 100) to guarantee success later down the line. They also interweave between Ophelia method and Peachy method depending on the current situation. In the end, all I needed was +14 so I was satisfied. 

## Experimental: One Layer Neural Network

Without knowing too much of deep learning, I was curious whether I could initiate a learning mechanism to optimize parameters (method, upgrade level, failstacks, extra resources) for minimum expected outcome. Since this was in June, I was dumb and blind. 

I wrote a neuron class featuring normalization of parameters into range [-1,1], randomized weights for the different parameters, and wrote a linear combination for the weight * parameter to simulate output. The goal was to find the best weights for the problem through population and evolution. I expected that, over time, if we breed the best weights of each generation and mutate them a little, we would find the best weights overall.

For fun, I called each agent a monkey. I trained 500 monkeys to enchant 1000 weapons each run. 1000 runs were used since we are dealing with probability. We need to normalize the expected outcome so that we don't deal with outliers.

In the end, the project was stopped before I could breed the monkeys together. Why? Because the results favored those monkeys that got lucky over a course of 1000 runs... even as I tried to normalize the outcome. All of the best data was written into a .txt file that I could parse for average outcome, methods used at evel upgrade level, etc. Some of these monkeys somehow managed to use an average of 44 weapons over the course of 1000 runs, which is a 20% decrease on costs! I also didn't feel that my neuron and linear combination were set up properly (in addition to only being one layer), so I decided to scrap it. Why compute like this when we already know a sufficent answer through brute force?

HOWEVER: the neural network did teach me some things about the upgrade system, believe it or not! 

1. Those who fail more early are rewarded with better outcomes in the end. This makes sense because at the beginning, no weapons are used. The more you fail at the beginning, the more failstacks you acquire without having to spend weapons. 
2. Ophelia method is the way to go. None of these monkeys ever used Peachy method since that would skew the resources closer to the guaranteed 55. If you are under 55, you want to remain under 55, not move towards 55. 
3. The difference between using 0, 1, and 2 extra weapons is miniscule. There were many different monkeys that used any of the above and still yielded great results. This is consistent with the brute force simulation as there is less than 0.2 difference between using 0 extra weapons and using 2 extra weapons. 

All of this knowledge was thanks to the parseable .txt log file.

## Conclusion

This was a fun project in probability! I certainly learned a lot and definitely used it to help me get into the raid. In the end, I actually used 43 weapons to get +14. My luck saved me 21.8% of the resoures...

My group was able to get rank S in the raid, putting us at rank 12 on our server at the time! I have since quit the game. 

<img src="https://nguyenjus.github.io/blog/assets/img/EnchantSuccess.jpg" width="50%" height="50%">
