## _Proximal Policy Optimization_ — A simple explanation

#### Author: Aman Y. Agarwal, founder of [DenseLayers.com](https://denselayers.com)

PPO falls under the [advantage actor-critic](a2c.md) (A2C) algorithm, with just a small tweak that makes a good difference in practice.

While learning to play the game, as you collect experience, your policy will get updated. But what if, after every couple of hours, your policy/playing style looked completely different from before? It would be as if you’re reacting too much, too quickly to the most recent game experience, instead of gradually updating your policy based over time based a broader, richer base of experiences.

Learning gradually and smoothly has been found to work better overall than learning in a “spiky” fashion where the policy swings too much. This is done by mandating that after each policy update, the new policy is proximal to the previous policy. Thus we have the fancy name: “Proximal Policy Optimization.”

In technical terms, the way we achieve this is by “clipping the objective function” such that the ratio between the policy after the update and the current policy would always be within a fixed range: (1-x to 1+x), with _x_ being a value that we can set as per our liking.

Because PPO is so stable, it has become a default favourite for training RL agents in complex, continuous environments (eg: games like Dota2).
