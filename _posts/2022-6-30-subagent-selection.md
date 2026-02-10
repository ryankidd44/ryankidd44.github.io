---
layout: post
title: "Selection processes for subagents"
description: "This post consists of rough thoughts on possible training processes that select for multi-agent architectures, or ``subagents'', in neural networks"
category: post
tags:
  - AI Safety
---

*This post consists of rough thoughts on possible training processes that select for multi-agent architectures, or "subagents", in neural networks. I deliberately ignore [delegative subagents that are instantiated by mesa-optimizers](https://www.lesswrong.com/posts/8RCCMStERhfkYZC8i/the-subagent-problem-is-really-hard) and instead* *focus on subagent architectures that arise due to "non-agentic" training processes alone.*

*Thanks to John Wentworth, Alkjash, Oly Sourbut, Oliver Zhang, Josh Clymer, Quintin Pope and Logan Riggs Smith for helpful feedback.*

Natural selection, in the process of optimizing for persistent genes, produced organisms that [optimize on their own](https://www.lesswrong.com/posts/8vpf46nLMDYPC6wA4/optimization-and-the-intelligence-explosion). However, evolution is imperfect local search and humans seem far from the "ideal blueprint" for optimizing gene persistence. In fact, human preferences indicate that we might be [behaviourally](https://www.lesswrong.com/s/pmHZDpak4NeRLLLCw) [more](https://www.lesswrong.com/s/ZbmRyDN8TCpBTZSip) [similar](https://www.alignmentforum.org/posts/3xF66BNSC5caZuKyC/why-subagents) to a collection of agents working towards a host of different objectives than a single [utility maximizing agent](https://www.lesswrong.com/tag/agent). If human brains or future AIs contain "subagents", how might this architecture have arisen? In this post, I list some selection processes that might produce systems with multi-agent architecture, containing redundantly expressed "agent modules" that individually act according to coherent preferences.

The possible selection processes I have so far identified are:

- Circuit depth prior favors parallelized agent modules;

- Circuit complexity prior favors goal factorization;

- Multi-agent games favor ecology internalization;

- Modularly varying goals favor specialized subagents; and

- Task performance favors adversarial subagents.

## Background

John Wentworth's [selection theorems](https://www.alignmentforum.org/posts/G2Lne2Fi7Qra5Lbuf/selection-theorems-a-program-for-understanding-agents) program aims to determine what properties "agent-like" systems must acquire under sufficiently high selection pressures. For example, natural selection seems to favor organisms that are well-adapted to operating in uncertain environments, conserve energy and experience pleasure and pain. Another common feature is modularity: organisms are composed of organs, cells and nerves/muscles (i.e. distinct sensor and effector units) that engage in essentially independent functions. Less obvious examples exist in the brain, such as the distinction between the [subcortex and neocortex](https://www.alignmentforum.org/posts/diruo47z32eprenTg/my-computational-framework-for-the-brain). Even less apparent modularity might exist in the form of cognitive subagents: cognitive processes that pursue distinct objectives such as resource acquisition or task-delegation, but act in concert to generate behavior.

As detailed in Wentworth's post '[Why Subagents?](https://www.alignmentforum.org/posts/3xF66BNSC5caZuKyC/why-subagents)', some systems of ordered preferences are better modeled as a committee of interacting agents than as a single agent. A committee of agents can exhibit coherent preferences, but remain indifferent between some world states and make different, yet coherent decisions given the past states of the system. For example, financial markets only permit trades in which all agents' utilities increase or are unchanged, but generally cannot be modeled as a single [agent](https://en.wikipedia.org/wiki/Representative_agent). Depending on the initial wealth distribution, a competitive financial market might reach radically different [Pareto-efficient](https://en.wikipedia.org/wiki/Pareto_efficiency) equilibria, where no agents are motivated to trade further. A competitive market cannot be [Dutch-booked](https://www.lesswrong.com/posts/RQpNHSiWaXTvDxt6R/coherent-decisions-imply-consistent-utilities), yet its behavior [generally](https://www.alignmentforum.org/posts/3xF66BNSC5caZuKyC/why-subagents#Path_Dependence) [cannot be explained](https://www.alignmentforum.org/posts/3xF66BNSC5caZuKyC/why-subagents#Path_Dependence) by a singular utility function over external states.

If an AI system is trained to exhibit subagent-like preferences (i.e. through human imitation) and also is exposed to strong selection pressure that favors "[optimizer](https://www.lesswrong.com/posts/znfkdCoHMANwqc2WE/the-ground-of-optimization-1)" architecture, it seems possible that the system will acquire multiple agent modules. These agent modules might individually perform optimization and pursue long-term goals, or take coherent actions without long-term planning. Collections of subagents might, in effect, "[cast votes](https://www.lesswrong.com/s/ZbmRyDN8TCpBTZSip/p/5gfqG3Xcopscta3st#Putting_together_a_toy_model)" or "[make trades](https://www.lesswrong.com/posts/3xF66BNSC5caZuKyC/why-subagents#Path_Dependence)" to determine model policy.

### Motivation

Why might it be useful to determine if certain selection processes produce multi-agent architectures?

-   If an AI learns and internalizes human values [by default](https://www.lesswrong.com/posts/Nwgdq6kHke5LY692J/alignment-by-default) and the type signature of human values is akin to a "market of subagents", we may produce AIs with multiple internal utility maximizers. It is not clear to me that if I increased the intelligence and communication ability of all my brain's (hypothetical) subagents, the resultant market of agents would cohere (e.g., via insurance contracts over all possible world states) into something that robustly pursued human [coherent extrapolated volition](https://www.lesswrong.com/tag/coherent-extrapolated-volition). If brains have subagents, [ambitious value learning](https://www.lesswrong.com/posts/5eX8ko7GCxwR5N9mN/what-is-ambitious-value-learning) proposals may need to consider whether the [Critch coalition](https://www.lesswrong.com/posts/7EupfLrZ63pbdyb9J/superrational-agents-kelly-bet-influence#Negotiable_RL) of unbounded utility maximizers with the appropriate subagent utility functions is still "aligned with human values".

-   The same selection processes that might have produced brain subagents may be present in neural network training processes. If we desire to build AIs without multi-agent architectures, perhaps to build [AIs without goals](https://www.lesswrong.com/posts/X2i9dQQK3gETCyqh2/chris-olah-s-views-on-agi-safety#Building_microscopes_not_agents) or AIs that are [inner-aligned](https://www.lesswrong.com/posts/pL56xPoniLvtMDQ4J/the-inner-alignment-problem) (i.e., terminally care about the base objective used in training), these selection processes may need to be circumvented. As a salient example, if brains have multi-agent architectures, these might contribute to "human inner misalignment" with the base objective of evolution due to each agent acting to optimize objectives that initially arose as proxies for genetic fitness.

## Possible selection processes

### Circuit depth prior favors parallelized agent modules

Unlike traditional feedforward neural networks with all-to-all connections between layers, [brains perform somewhat architecturally modular computation](https://link.springer.com/referenceworkentry/10.1007/978-3-319-16999-6_2422-1). It might be advantageous to redundantly specify "agent-like" optimization processes in the brain if computing the optimal policy for a goal in a given environment hinges on a hidden environmental variable and fast action is critical. The selection pressure described here enforces something like a "[speed prior](https://www.alignmentforum.org/posts/GC69Hmc6ZQDM9xC3w/musings-on-the-speed-prior)" on brain architecture: fast, parallel computations are advantageous.

As a naive example, consider an environment state that is potentially highly dangerous for an organism and requires prompt action: either "fight" or "flee." However, the preferred type of action depends on an unknown environmental variable: "predator strength/speed." The organism has little time to develop optimal policies for executing "fight" or "flee," and choosing the wrong strategy could be fatal. Therefore, the optimal way for the organism to prepare for the impending crux is to delegate part of its cognitive architecture towards finding the optimal policy for "flee" and part towards finding the optimal policy for "fight," and then defer to the appropriate policy as soon as it determines "predator strength/speed." If both policies require "agent-like" architecture (i.e., some process that coherently ranks candidate policies and perhaps performs iterative search), this might select for multiple agent modules that perform parallel computation. Subagent architectures that first evolved via this selection process might be later incorporated into more complex general planning circuits if they perform sufficiently well at evolving tasks.

As in the [gooder regulator theorem](https://www.alignmentforum.org/posts/Dx9LoqsEh3gHNJMDk/fixing-the-good-regulator-theorem), this subagent partitioning is contingent on a hidden environmental variable revealed late in runtime. For the selection pressure to be sufficiently strong, the optimal policies under different hidden variables must require sufficiently different simulation; i.e., most of the computation required for a given optimal policy is conditional on a particular value of the hidden variable. If the organism had more time (i.e., less of a speed prior), perhaps it could reuse the same cognitive architecture for both options. If computing either optimal policy in the environment was insufficiently hard, perhaps "agent-like" optimizing circuits would not be necessary.

The occurrence of this type of policy modularity could be tested in a neural network by instantiating a game where most of the decision-relevant information is revealed to a network that is required to compute and store a latent state in the second last layer of the network. A random environmental variable that heavily conditions the optimal policy is revealed to the last layer of the network, right before loss calculation. If this selection process is strong, the architecture might develop strong modularity above the final layer, which essentially might perform a gate operation, choosing one of the precomputed policies represented in the latent state, conditioned on the hidden variable. Assuming that the model cannot learn an "agent-like optimizing function" and call it independently in two parts of the network, I suspect such an agent-like function would be redundantly expressed in the model. Even if a "world model" is too expensive to express redundantly, I expect subagents with different utility functions could coexist with access to the same "backend" world model.

#### Open questions

-   Are modern neural networks sufficiently shallow that parallel agents are favored?

-   Does parallel processing in the human brain meet the criteria for "parallel agents"?

-   Given that the proposed test is somewhat artificial in how the hidden bit is withheld to the last layer, what reinforcement learning test should produce subagents according to this selection process?

### Circuit complexity prior favors goal factorization

I think that if brains implement something like a circuit complexity prior and there are lots of [modularly varying goals](https://www.lesswrong.com/posts/JBFHzfPkXHB2XfDGj/evolution-of-modularity) in the environment, an easily-reachable-through-training representation of a complex utility function might be a set of short "agent-like" circuits that are "switched between" by some sort of global overseer. If specifying each goal requires sufficiently independent circuitry due to modularly varying goals, then it might be easier for the architecture's inductive biases to separately find the cognitive circuitry for a set of goals than to create one large circuit that perfectly represents the optimal goal. This selection pressure favors a "scarcity of channels" between "relatively abundant modules" (credit to John Wentworth for this framing).

If smaller circuits have larger densities in the [parameter tangent space](https://www.lesswrong.com/posts/i9p5KWNWcthccsxqm/updating-the-lottery-ticket-hypothesis) of a neural network, I suspect that SGD is more likely to learn a set of smaller circuits than the single large circuit they approximate. Smaller circuits are probably denser in the space of reachable circuits because they require fewer parameters to specify and thus constrain the space of total parameters less than larger circuits. In other words, the volume of parameter space occupied by all models that contain a given small circuit is generally much larger than that for a given large circuit. Additionally, the volume of parameter space occupied by all models that contain, for example, four small independent circuits, each encoding one of four goals, might be much larger than the volume occupied by all models that contain a single large circuit that satisfies all four goals, if the latter circuit is significantly larger than each small circuit.

Unlike the previous selection story, no temporarily hidden information is assumed; this selection process is entirely driven by modularly varying goals and a bias for smaller circuit complexity. In fact, this selection pressure represents a tradeoff between the factorizability of a function and the inductive bias for smaller circuits. Environmental goals with imperfect modularity might still be approximated well enough by modular architecture such that the bias for small circuits dominates.

A possible experiment to test this aspect of modularity is to see if, as neural network depth is increased, modularity is enforced given a sufficiently "factorizable" goal. I'm imagining a goal that is optimally satisfied by computing a function that has high circuit complexity but is well-approximated by a series of small circuits that all compute functions, which are then combined in a later layer. The relative abundance of smaller circuits should increase with network size and goal factorizability.

#### Open questions

-   What types of goals are factorizable?

-   Are multi-agent systems with factorized goals empirically likely to occur?

-   How many neural network parameters are required to specify a "goal-directed agent"?

-   How much more abundant are smaller circuits than larger circuits as a function of network size?

### Multi-agent games favor ecology internalization

Natural environments contain many competing organisms that can often be approximated as agents: they take actions according to some coherent ranking over preferences such as a utility function. To simulate complicated ecological interactions between agents and make predictions useful to survival, brains might have acquired compressed representations of multi-agent systems that can model agent interactions in arbitrary environments. If these minimal models are incorporated into the "policy" that the brain acts on, the organism may act as if it is governed by a committee of subagents. I call such a process "ecology internalization". This selection pressure is inspired by the [natural abstraction hypothesis](https://www.lesswrong.com/posts/Nwgdq6kHke5LY692J/alignment-by-default#Unsupervised__Natural_Abstractions).

As a naive example, consider the complex social reasoning "games" early humans were faced with, like mutually acceptable resource allocation among tribe members or dispute resolution. Given a broad enough class of games, perhaps the best method for a brain to compute decision-relevant information about how external "agent-like" systems will behave in a given environment is by internally simulating agent dynamics, rather than using simple heuristics. As in the [gooder regulator theorem](https://www.alignmentforum.org/posts/Dx9LoqsEh3gHNJMDk/fixing-the-good-regulator-theorem), one could imagine a hidden environmental variable that "chooses" a game type, which the external agents then play. If "internally represent and simulate agents as necessary for predictions" is an [easily reached](https://www.lesswrong.com/s/r9tYkB2a8Fp4DN8yB/p/q2rCMHNXazALgQpGH#fn-EwoZYq7rcmQ38kmiy-7) and high-performing policy for performance in sufficiently complex agent-filled environments, ecology internalization seems plausible.

Acquiring subagents in prediction systems might serve as a good minimal prediction architecture if agents in the environment choose their actions according to predictions of each other. Imagine a game played by two external agents where the game type (e.g. cooperation vs. anticooperation) is determined by a random environmental variable $Y$. Perhaps the agents would individually prefer to cooperate in times of strong research plenitude and anticooperate in times of strong resource scarcity, but have different preferences for at least some world states. We might assume that the agents learn strategies that correspond to optimal play (i.e. mixed strategy Nash equilibria). A good model of the joint behavior of these agents will account for the strategies the agents will employ in each game and make predictions that depend on the environmental random variable $Y$. On observing $Y$, an organism could run its internalized ecology simulation, which might amount to an [iterative search for a Nash equilibrium](https://www.cs.ubc.ca/~hutter/earg/papers04-05/computing-nash-eq.pdf) using callable agent modules.

A ML model that observes the world might acquire "[better generalization through search](https://www.lesswrong.com/s/r9tYkB2a8Fp4DN8yB/p/q2rCMHNXazALgQpGH#2_1__The_task)" by learning multiple search objectives that correspond to the agents in the world who sufficiently impact the model's performance. Predicting how ecosystems of humans behave in general environments might be compactly modeled by learning the architecture of multi-human optimization processes and calling this "multi-human function" on various inputs at runtime. Rather than learning a look-up table of action-value pairs or a set of simple heuristics, the ML model might internally acquire models of the individual human utility functions that together predict multi-human behavior. In this instance, multi-agent behaviour might be simply modelled by acquiring subagent-like architecture in the value function. If this selection process occurs, we might expect a "phase transition" in predictive model architecture as we scale from micro- to macro-economic regimes (where predicting multi-agent dynamics can be approximated by a "[mean-field](https://en.wikipedia.org/wiki/Mean-field_theory)" theory).

#### Open questions

-   What are the characteristics of multi-agent games where predicting the actions of multiple external optimizers incentivizes internalizing multiple optimizers instead of one?

-   What computational limitations make "internalize multiple optimizers" useful for prediction?

-   Under what conditions are agents (potentially learned optimizers) that are acquired in predictive architecture incorporated into a model's "value function" or ["decide" mapping](https://www.lesswrong.com/posts/LBNjeGaJZw7QdybMw/agents-over-cartesian-world-models)?

### Modularly varying goals favor specialized subagents

As an organism is exposed to new environments, the selection pressure that it is subject to changes. For example, if a particular selection pressure (e.g. food acquisition) is held constant and another time-competing pressure requiring different cognitive machinery (e.g. predation) is intermittently applied, an animal might acquire separate cognitive subsystems to handle these drives if this is less training-expensive (i.e. more easily reachable by local search) than incorporating new goals into a single optimizing circuit. Similarly, mutations that are maladaptive to only one of the predator-hiding or food-finding subsystems are less catastrophic to an individual animal than mutations that compromise both systems. Thus, [modular subsystems](https://www.lesswrong.com/posts/JBFHzfPkXHB2XfDGj/evolution-of-modularity) might be reinforced by strong, random selection pressure that acts on local "chunks" of cognition.

#### Open questions

-   Do modularly varying goals [favor modular systems](https://www.lesswrong.com/s/ApA5XmewGQ8wSrv5C)?

-   Does [SGD's bias](https://www.alignmentforum.org/posts/ej2r2JADoWiEtxkCd/sgd-s-bias) favour modular systems?

-   Is the occurrence of specialized subagents "path-dependent"? Are specialized subagents only acquired sequentially (when selection pressures modularly vary in time), or do consistently factorizable environments (i.e., those with low mutual information between chunks) favor specialized subagents too?

### Task performance favors adversarial subagents

Subagent-like modularity might offer performance advantages to some cognitive processes in a compute-constrained system. For example, [some incentive landscapes don't map well onto a simple reward function](https://www.alignmentforum.org/posts/frApEhpyKQAcFvbXJ/reward-is-not-enough#1__Incentive_landscapes_that_can_t_feasibly_be_induced_by_a_reward_function), but might be constrained by several independent reward functions operating in tandem. The human brain [might employ](https://www.alignmentforum.org/posts/frApEhpyKQAcFvbXJ/reward-is-not-enough#2__Wishful_thinking) something like an [actor-critic](https://www.alignmentforum.org/posts/Ajcq9xWi2fmgn8RBJ/the-credit-assignment-problem#Actor_Critic) reinforcement learning architecture to avoid [wireheading](https://www.alignmentforum.org/tag/wireheading) while seeking rewards. Human psychological processes might factor into something like an [internal family systems model](https://www.lesswrong.com/s/ZbmRyDN8TCpBTZSip/p/YXBpBCNC66daaofoY). Adversarial processes, such as [GANs](https://en.wikipedia.org/wiki/Generative_adversarial_network), [debate](https://openai.com/blog/debate/) and [red-teaming](https://en.wikipedia.org/wiki/Red_team), are effective at exposing flaws and building more robust models. If task performance is strongly selected for and adversarial set-ups are high-performing, adversarial subagents seem likely, architecture permitting.

#### Open questions

-   Do actor-critic systems emerge spontaneously in a reinforcement learning context?

-   Is [reward enough](https://www.sciencedirect.com/science/article/pii/S0004370221000862?via%3Dihub)?

-   Does the human brain perform red-teaming and, if so, to what recursive depth?

-   What tasks strongly favor red-teaming?

## Conclusion

This is still a very rough outline of the selection processes that might contribute to subagent architectures. I appreciate all feedback and would love any support in addressing what I see as the open questions in this line of research. I do not believe that the existence of subagents in the human brain is settled, or even necessarily a concept that "carves reality at the joints" (e.g., see [here](https://www.lesswrong.com/posts/H5iGhDhQBtoDpCBZ2/announcing-the-alignment-of-complex-systems-research-group?commentId=sAhReJfp2SkvACwJQ)), but hope that the discussion of subagent selection processes here might be useful.

---

This article was posted on [LessWrong](https://www.lesswrong.com/posts/d4hw4FBX9YXHGFBWQ/selection-processes-for-subagents).
