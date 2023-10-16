## _Advantage Actor Critic Methods_ — A simple explanation

#### Author: Aman Y. Agarwal, founder of [DenseLayers.com](https://denselayers.com)


Actor-critic methods are a family of algorithms united by the same philosophy. In terms of implementation, the most popular variant is the _“Advantage Actor-Critic”_ algorithm. Here’s how it works.

Recall that at any given state _s_ in the game, our agent chooses an action a by sampling from a probability distribution (output of the policy).

Now, any action choice naturally has a different value — i.e. some actions are more likely to lead to a high reward/victory than others.

Let’s say that at a given state _s_, the agent expects a total reward of 5.0 with action _a<sub>1</sub>_, 6.0 with _a<sub>2</sub>_, and 2.0 with _a<sub>3</sub>_.

In this example, on average, the agent gets a reward of 4.33 by following its current policy. Therefore, the advantage of taking action _a<sub>1</sub>_ versus the average is 5–4.33 = 0.67. For _a<sub>2</sub>_, the advantage is 1.67, and for _a<sub>3</sub>_, it’s -2.33.

That’s it — the Advantage function, represented as _A(s,a)_, is the _extra_ reward expected by choosing a certain action _a_ in state _s_ compared to the “average.” In advantage actor-critic, when comparing actions, we rely on this advantage value.

Why is this helpful? Intuitively, this is done to force the model to strive to do better and better than average; to only take the most optimal actions, as opposed to being satisfied with picking actions as long as they lead to a positive reward.
