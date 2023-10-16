## _Actor Critic Methods_ — A simple explanation

#### Author: Aman Y. Agarwal, founder of [DenseLayers.com](https://denselayers.com)


As a human, when you get better at playing a game (say soccer or boxing), isn't the improvement also usually accompanied by getting better at _evaluating_ games — i.e. answering questions such as “which side is doing better” at any given point in a game? 

It also goes the other way around — being good at evaluating your own performance during a game also enables you to _coach yourself_, thus being able to try new things and get better over time – without necessarily needing external supervision.

And that is the fundamental intuition behind "actor critic" methods. In essence, being your own critic helps you grow as an actor, growing as an actor makes you a better critic, and the cycle continues. Turns out, we can use this to learn a game from scratch.

Even when you play a game (let's say, a video game like Dota2) for the first time, you don’t have to wait for the end of a game to start improving your skills. While playing, you already have a _feeling_ to judge how well you’re doing, to use that to slowly improve the way you play. At the end of the game, you’re a better player than when you started, regardless of the actual score.

In a sense, you relied on your internal judgment) to update your own “policy” (i.e. strategy for choosing actions) instead of the final score.

Even before you’ve finished the first game (and seen the final result of “win or lose”), you may already learned a fair bit about making better decisions and taking better actions, based on the experience and the rewards you collect along the way.

**Here's how it works in Reinforcement Learning.**

The policy of the agent outputs two things:

    1. Actions (i.e. what action to take in the game)
    
    2. Value Function: the model also makes its own estimate of “how well it’s doing in the game.” We call this the “value” of being in that state, at that timestep. The higher this value, the higher the total “reward” the agent expects to earn in the game from that point on till the end (and the more likely it expects to win the game).

At any given time, we let the agent play the game as it normally would — i.e. by sampling actions from its current policy. At first, we let the agent use its own judgment to improve its gameplay — i.e. it updates its policy based on its value estimate. So in a sense, the agent is always trying to learn a policy that does the best by its own standards. It is both the ACTOR and the CRITIC.

The other important aspect of training is improving your judgment — that is, to improve the accuracy of your value function.

Over time, as you play more games to the finish and observe the actual reward values, you can compare them to the predicted values, and thus get better at estimating the value of any given state of the game. This is called the “value update.”

And since the policy is chasing after the value function, improving the value function over time means also improving the policy function — which is what we’re after. We just want the best possible policy model.

This training method, where you constantly improve your policy based on your value estimations (as opposed to always waiting for the end of the game to learn anything) is called the Actor-Critic method. 

