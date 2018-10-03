Alex Gavryushkin
Centre for Computational Evolution
The University of Auckland, NZ

This is a joint work in progress with Erick Matsen and Chris Whidden from Fred Hutchinson Cancer Research Center, Seattle, WA.
Based on an earlier work with and communicated by Alexei Drummond, the University of Auckland.


## Nearest neighbors of phylogenetic time-trees

With phylogenetic methods being employed in various areas of science, the information carried by the tree may have substantially different meanings.
Examples include gene trees, species trees, transmission trees, language trees, etc.
In many of these applications, the concept of *time* explicitly presents in the data and often is an objective for phylogenetic *time-tree* inference.
By time here we mean actual absolute time that can be put on a calendar, as opposed to relative measures that entangle time and mutation rates.

An important property that distinguishes a time-tree from a classical phylogenetic tree is that all nodes of the tree (divergence and sample events) are ranked according to their time.
For example, the fact that the MRCA of human and chimp is younger than that of elephant and hyrax is expressed in a time-tree but not in a classical tree.
Furthermore, incorporating time into Bayesian tree search algorithms greatly improves their efficiency (e.g. MCMC moves in BEAST).

Many phylogenetic comparative methods, as well as tree search methods, use elementary modifications of trees to explore the space.
The most known and widely used modifications presently are NNI, SPR, and TBR.
They constitute the main bottleneck for computations.

Surprisingly little is known about elementary modifications of time-trees.
Indeed, there exists no standard coordinate system for continuous time-trees that induces a natural notion of an elementary modification for discrete time-trees.
Furthermore, unlike traditional tree discretizations such as the NNI graph there is not yet any way to express time information in graph structure.

In this work, we suggest an approach to fill this gap by providing a novel coordinate system for phylogenetic time-trees.
This system scales naturally from continuous to discrete trees by hierarchically approximating continuous time by discrete time segments.
Although elementary moves between trees are inherited from the NNI move, geometric and algorithmic properties of the moves are greatly different.

In this talk, I will introduce the coordinate system and motivate it by popular applications in computational phylogenetics.
I will compare the system with classical phylogenetic trees and demonstrate its algorithmic and statistical potential.
I will finish with a list of open problems that have a wide range of applications in phylogenetics and beyond.

