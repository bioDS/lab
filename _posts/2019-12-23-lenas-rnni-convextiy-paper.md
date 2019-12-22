---
layout: post
title:  "Geometry of ranked nearest neighbour interchange space of phylogenetic trees"
date:   2019-12-23 10:30:00 +1300
categories: papers
---

A few years ago [Alexei Drummond](https://alexeidrummond.org/) and I started thinking about the [space of phylogenetic time trees](https://doi.org/10.1016/j.jtbi.2016.05.001).
Back then we thought it would take a quick mathematical fix to adapt the [space of classical phylogenetic trees](https://doi.org/10.1006/aama.2001.0759) to time trees.
It's just a matter of parametrisation how you interpret branch lengths, as substitutions per site or (calendar) time to divergence, after all.
As it quickly turned out, thing were quite a bit more complicated.
First, we quickly realised that, unlike for classical phylogenetic trees, there is no unique way to decide what the meaning of a branch length is for time trees &mdash; one option is to consider time differences between divergence events (nodes of trees) and another is to consider the actual times of divergence events.
Second, we notices that the (algebraic geometry) approaches [developed for classical trees](https://doi.org/10.1006/aama.2001.0759)are not going to work for time trees for reasons that go deep in [hyperbolic group theory](https://alexeidrummond.org/) &mdash; specially, there is no characterisation of non-positively curved simplicial complexes in the way there is Gromov's theorem to quickly check whether a cubical complex is non-positively curved.
This is a fascinating and still open problem that connects geometric group theory with applied phylogenetics, so I encourage reading [our paper with Alexei](https://doi.org/10.1016/j.jtbi.2016.05.001) to learn more.

At that point I felt somewhat frustrated mostly because it didn't look like the problem was going to be solved in the general setting by someone from the algebraic geometry or geometric group theory community, and I myself had spent enough time thinking about the partial instance of the problem in the case of phylogenetic time trees.
Around that time, I was visiting [Erick Matsen](https://matsen.fhcrc.org/) and [Chris Whidden](https://web.cs.dal.ca/~whidden/) in Seattle to work on random walk over phylogenetic graphs, for example, the nearest neighbour interchange (NNI) graph.
I was impressed by how hard it was to work with NNI, mostly because the NNI operation on trees often requires you to do very strange tricks if you want to take a shortest path to go from one tree to another be modifying your trees only using this operation.
This quickly triggered the memories of my battles with simplicial complexes because the NNI graph is the discrete component of the classical [continuous tree space](https://doi.org/10.1006/aama.2001.0759).
What is the discrete component of the [continuous time tree space](https://doi.org/10.1016/j.jtbi.2016.05.001).
Surely, it was to be some kind of generalisation of NNI to ranked trees!
Can we use the complexity of the NNI graph to prove that this generalisation is also hard?
Would the hardness of this generalisation imply that the continuous time trees space is also hard to deal with computationally?
Fortunately for me, Erick and Chris were interested enough to try and think about these questions, so we've written a [paper](https://doi.org/10.1007/s00285-017-1167-9) where we introduced all these things properly and came up with the ranked nearest neighbour interchange (RNNI) graph on ranked phylogenetic trees.
Apart from mathematical curiosity, our motivation was fuelled by the fact that RNNI modifications are the type of operations phylogenetic tree search algorithms are using to solve various optimisation problems, so if the complexity of the graph has an immediate impact on software phylogeneticists use every day.
We didn't get very far with this complexity question but we did show that the geometry and algorithmic complexity of RNNI would be really hard if at all possible to figure out using the comprehensive theory developed for NNI.

I came back to Auckland quite stoked about this development.
It was very clear to me back then that it either would require some novel and exiting result to transfer the NNI theory to the RNNI space, or the latter is actually simpler than the former.
I was trying hard to hold off my excitement about the latter possibility, so decided that I should just try and prove all the basic things that were known about NNI in the RNNI space.
And this was when I got very lucky again because during the time [Lena](/people/) as visiting Auckland for the summer and planning what to do next with her education.
I suggested her to think about these questions.
In fact, now that I think about those days, I pour all the messy thoughts and ideas I has about RNNI on her, but she somehow managed to make some sense out of all that and immediately prove that Erick, Chris, and I were quite naive in conjecturing RNNI might behave really well.
Specifically, she found a counter-example to our [Split Theorem conjecture](https://doi.org/10.1007/s00285-017-1167-9), confirmed our feeling that understanding the geometry of the space is the key to settling its algorithmic complexity, and decided to write a whole MSc on this topic.

Following Lena's [outstanding MSc thesis]({% post_url 2018-09-13-welcome-lena %}), she has recently gathered the most exciting bits of her work in Greifswald and at Max Planck and written a [paper that we have just published on bioRxiv](https://doi.org/10.1101/2019.12.19.883603).
