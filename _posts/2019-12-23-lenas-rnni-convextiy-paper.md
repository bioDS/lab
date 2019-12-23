---
layout: post
title:  "Geometry of ranked nearest neighbour interchange space of phylogenetic trees"
date:   2019-12-23 10:30:00 +1300
categories: papers
---

A few years ago [Alexei Drummond](https://alexeidrummond.org/) and I started thinking about the [space of phylogenetic time trees](https://doi.org/10.1016/j.jtbi.2016.05.001).
Back then we thought it would take a quick mathematical fix to adapt the [space of classical phylogenetic trees](https://doi.org/10.1006/aama.2001.0759) to time trees.
It's just a matter of parametrisation how you interpret branch lengths, as substitutions per site or (calendar) time to divergence, after all.
As it turned out though, things were quite a bit more complicated.
First, we quickly realised that, unlike for classical phylogenetic trees, there is no unique way to decide what the meaning of a branch length is for time trees &mdash; one option is to consider time differences between divergence events (nodes of trees) and another is to consider the actual times of divergence events.
Second, we notices that the (algebraic geometry) approaches [developed for classical trees](https://doi.org/10.1006/aama.2001.0759) are not going to work for time trees for reasons that go deep in [hyperbolic group theory](https://alexeidrummond.org/) &mdash; specially, there is no characterisation of non-positively curved simplicial complexes in the way there is Gromov's theorem to easily check whether or not a cubical complex is non-positively curved.
This is a fascinating and still open problem that connects geometric group theory with applied phylogenetics, so I encourage reading [our paper with Alexei](https://doi.org/10.1016/j.jtbi.2016.05.001) to learn more.

At that point I felt somewhat frustrated mostly because it didn't look like the problem was going to be solved in the general setting by someone from the algebraic geometry or geometric group theory community, and I myself had spent enough time thinking about the partial instance of the problem in the case of phylogenetic time trees.
Around that time, I was visiting [Erick Matsen](https://matsen.fhcrc.org/) and [Chris Whidden](https://web.cs.dal.ca/~whidden/) in Seattle to work on random walks over phylogenetic graphs, for example, the nearest neighbour interchange (NNI) graph.
I was impressed by how hard it was to work with NNI, mostly because the NNI operation on trees often requires you to do very strange tricks if you want to take a shortest path to go from one tree to another by modifying your trees only using this operation.
This quickly triggered the memories of my battles with simplicial complexes because the NNI graph is the discrete component of the classical [continuous tree space](https://doi.org/10.1006/aama.2001.0759).
What is the discrete component of the [continuous time tree space](https://doi.org/10.1016/j.jtbi.2016.05.001)?
Surely it had to be some kind of generalisation of NNI to ranked trees!
Can we use the complexity of the NNI graph to prove that this generalisation is also hard?
Would the hardness of this generalisation imply that the continuous time trees space is also hard to deal with computationally?
Fortunately for me, Erick and Chris were interested enough to try and think about these questions, so we've written a [paper](https://doi.org/10.1007/s00285-017-1167-9) where we introduced all these things properly and came up with the ranked nearest neighbour interchange (RNNI) graph on ranked phylogenetic trees.
Erick has [blogged](https://matsen.fredhutch.org/general/2016/07/11/discrete-time-tree.html) about that paper before.
Apart from mathematical curiosity, our motivation was fuelled by the fact that RNNI modifications are the type of operation phylogenetic time tree search algorithms are using to solve various optimisation problems, so the complexity of the graph has an immediate impact on various software packages phylogeneticists use every day.
We didn't get very far with this complexity question but we did show that the geometry and algorithmic complexity of RNNI would be really hard if at all possible to figure out using only the (comprehensive) theory developed for NNI.
So we were onto something that required new non-trivial mathematics and algorithms.

I came back to Auckland quite stoked about this development.
It was very clear to me back then that it either would require some novel and exiting result to transfer the NNI theory to the RNNI space, or the latter is actually simpler than the former.
I was trying hard to hold off my excitement about the latter possibility, so decided that I should just try and prove all the basic things that were known about NNI in the RNNI space.
And this was when I got very lucky again because during the time [Lena](/people/) was visiting Auckland for the summer and planning what to do next with her education.
I suggested her to think about these questions.
In fact, I just poured all the messy thoughts and ideas I had about RNNI on her, but she still managed to make some sense of all that and immediately prove that Erick, Chris, and I were quite naive in conjecturing that RNNI might behave really well.
Specifically, she found a counter-example to our Split Theorem ([Conjecture 9 in our paper](https://doi.org/10.1007/s00285-017-1167-9)), confirmed our feeling that understanding the geometry of the space is the key to settling its algorithmic complexity, and decided to write a whole MSc on this topic.

Following Lena's [outstanding MSc thesis]({% post_url 2018-09-13-welcome-lena %}), she has recently gathered the most exciting bits of her work in Greifswald and at Max Planck and written a [paper that we have just published on bioRxiv](https://doi.org/10.1101/2019.12.19.883603).
In the paper we continue the study of geometric properties of the RNNI graph, which is just the classical NNI graph, where vertices are phylogenetic trees and edges are NNI moves, extended to ranked trees by adding rank moves and requiring that NNI moves are only performed on nodes of consecutive ranks:
![RNNI](/assets/RNNI.svg)<br>
Here for instance, if we start from the middle tree in the top row and want to perform an NNI move on the edge adjacent to the parent of 3 and 4, we have to first do the displayed rank move and go the tree on the left.
As we show in our new [paper](https://doi.org/10.1101/2019.12.19.883603) this requirement makes many strangely looking NNI tricks impossible in RNNI.
For example, if you have two caterpillar trees in NNI and you want to find the smallest number of NNI moves to convert one into the other, what you need to do is to consider all kinds of odd combinations of leaves grouped together and moved around the tree to economise on some additional NNI moves that move leaves independently.
Here is the simplest example of when this kind of behaviour is happening:
![RNNI VS NNI](/assets/NNI_vs_RNNI.svg)<br>
Note that you cannot do the move indicated by the dashed line in RNNI, so this trick doesn't go through there.
As we have shown in the paper, this is actually an example for a more general phenomenon &mdash; some classes of trees, such as caterpillar trees, are convex in RNNI but not in NNI.
Being a convex class simply means that you can go from one tree to another by a shortest path without leaving the class.

At that stage it was obvious to us that these and similar geometric properties have immediate algorithmic consequences.
Indeed, the convexity example demonstrates that if you want to find a shortest path from one tree to another and your trees are in some nice class, all you have to do is to find such a path _within_ the class, which, in case of caterpillar trees, for example, is trivial.

Prior to our decision to study the geometry of the RNNI space, Lena has been developing various computational approaches and experiments to see how far our conjectures hold if we consider bigger and bigger trees.
During that period, she's come up with some really nice heuristics to navigate the space.
For example, she's designed an algorithm called MDTree (Algorithm 3 in our [paper](https://doi.org/10.1101/2019.12.19.883603)) that produces a tree as dissimilar to a given one as possible.
We knew that all these heuristics produced the exactly correct results for small trees (because spaces on trees with up to 6 taxa can be stored in laptop's memory) but we just weren't sure how far one has to go to produce a counter-example if one exists.
We were quite positive though that those counter-examples must exist.
That was because all Lena's algorithms were greedy &qdesh; they make decision on whatever seems to the best thing to do at the moment the decision has to be taken.
The trick above when making clusters of leaves and moving them around the tree is a beneficial strategy, is an example where a greedy algorithm wouldn't work, as you have to pay some NNI moves to make clusters in order to economise in the future.
Remember that back then we didn't know about the convexity and other nice geometric properties in RNNI &qdesh; we were pessimistically looking for counter-examples.
Imagine our surprise when we discovered that _all_ those greedy algorithms give the exact solution for _arbitrarily_ large trees.
Following the hangover from this discovery, we decided to honour the importance of these algorithms for our study of the geometry and structure the paper in the unusual way it is currently structured &qdash; we first introduce the algorithms and then use those algorithms to study the geometry of the space, proving on the way that the algorithms are correct.

A very careful reader might have noticed that the 6 taxa limit in the previous paragraph is inconsistent with what we are reporting in the [paper](https://doi.org/10.1101/2019.12.19.883603).
This is because much has changed since those early attempts.
In particular, our team was on the way enhanced by [Kieran](/kieran/), who, among other things, improved our computational experiments and in particular lifted this to 7 taxa &mdash; remember that there are many more trees in RNNI than in NNI, so 7 taxa is not an easy ride.

Where next?
I am personally very much convinced that the RNNI space has many hidden surprises ready for us to discover.
Upon finishing this paper, I've become of an opinion that some of those discoveries don't have to wait for 25 years, the way [it's happen in NNI](https://paperpile.com/app/p/5ede24e6-5ba6-0ae9-8772-f702335e040b).
Although, as we have shown in the paper, the strong version of the split theorem doesn't hold in RNNI, the weak version might.
Furthermore, the cluster theorem (Conjecture 10 in the [paper](https://doi.org/10.1101/2019.12.19.883603)) is very likely to be true in the light of our results.
Although, even if true, the cluster theorem doesn't necessarily lead to practical algorithms useful in everyday computational phylogenetics (e.g. the Subtree Prune and Regraft operation gives an example of a tree space where the split theorem doesn't come with efficient algorithms), the _reason_ it might be true is the greedy nature of all the approaches that work in RNNI and don't work in NNI.

I hence am positive that these mysterious hopes and conjecture together with our results will aspire more mathematical development of this area in 2020 and years to come.
