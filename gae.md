## _Generalized Advantage Estimation_ — A simple explanation

#### Author: Aman Y. Agarwal, founder of [DenseLayers.com](https://denselayers.com)


GAE is yet another little technique used to make training more stable, and to ensure that the model continues to improve over time — it helps with credit assignment, which we discussed earlier.

Recall that in actor-critic methods, we have a value function that enables the agent to use its own prior experience to judge how good its current position in the game is. We must update both the policy and the value function.

Now, if we wanted the most real, objective measure of the value of taking an action, there’s no other way but to actually play the game to finish and observe all the rewards, right? This way of calculation is the least biased by the agent’s prior experience. Let’s put this in numbers quickly.

We’re using policy _π_ to sample actions and collect incremental rewards _r_ in the game at each state _s_.

At a given state s, the total reward expected from taking a certain action _a_ is the immediate reward _r0_, PLUS the sum of future rewards in the game:

_R = r1 + r2 + r3 + r4 + …._

So far so good?

But we also know that future rewards are less and less dependent on our current action, and more dependent on future actions. Therefore, we discount the future rewards progressively using a discounting factor γ (gamma).

So, value of taking action _a_ in state _s_ = _Q(s,a)_ = _“Expectation of” [r0 + γ.r1 + γ².r2 + γ³.r3 + ….]_

If _γ=0_, then only _r0_ gets counted, and the model doesn’t assign credit for any future rewards to this action. (But that wouldn’t work for any game that requires any semblance of a strategy.)

If _γ=1_, then every single future reward gets the same weight as the current reward.

This was about discounting rewards. (P.S. If you’re familiar with finance, and know how to use discounted cash flows to calculate the present value of an asset, it’s a very similar concept.)

But of course, here we completely ignored the value function, which would make training extremely slow — without using prior experience/self-judgment to improve while playing, the agent wastes a lot of time collecting gaming experience with dud policies that only get updated once in a while.

So, let’s say we decided to do a combination of both: to train the agent based on both real, observed rewards AND the value function.

Now, we can choose how many steps we want to look ahead at for real rewards, with the rest being approximated by the value function **V**.

This makes our training more biased (by the agent’s prior experience), but reduces the variance (i.e. makes the agent learn faster and do better in the short term). So we call this a “variance-reduction technique.” Ring a bell? :)

As we saw earlier,

_Q(s,a) = E[r0 + γ.r1 + γ².r2 + γ³.r3 + …. ]_

But we can choose to look ahead only for a few rewards, say until k=4 timesteps, and use V(s) to replace the rest:

_Q(s,a) = E[r0 + γ.r1 + γ².r2 + γ³.r3 + γ4.V(s4)]_

If we chose k=10:

_Q(s,a) = E[r0 + γ.r1 + γ².r2 + γ³.r3 + γ⁴.r4 +…. γ¹⁰.V(s10)]_

And if we chose k=0:

_Q(s,a) = E[r0 + γ.V(s1)]_

So you see, the higher our “lookahead”, the longer we rely on real rewards. If we only wanted to use real rewards, we’d do _k=∞_ or something.

Now, someone came up with an idea. Instead of having to pick a single value of _k_, how about doing a weighted average of multiple _k_ values?

We also remove the average from our calculations, because we only care about the advantage of choosing a particular move.

By doing that, our advantage of a particular move becomes:

_A(s,a) = A(k=0) + λ.A(k=1) + λ².A(k=2) + λ³.A(k=3) + …_

where _λ_ is another weighing factor to discount the higher values of _k_.

This is called Generalized Advantage Estimation. It’s a way to combine past experience with actual observed rewards while training, to have the best balance between bias and variance.

It’s yet another little technique to make sure the training is stable and gradual. It might feel like we’re splitting hairs here, doing all these little tweaks to algorithms, but here’s the thing — when you’re spending millions of dollars on an experiment, you want to squeeze as much value from your money as possible. Training time in ML isn’t free, so it behoves us to make use of as many tricks as possible to ensure that training is fruitful.
