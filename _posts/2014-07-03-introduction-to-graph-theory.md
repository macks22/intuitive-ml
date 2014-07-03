---
title: Introductory Notes On Graph Theory
author: Mack Sweeney
layout: post
---

This post contains notes which can serve as a high-level introduction to the
concepts of graph theory. It is organized into three sections, which currently
correspond to the number of 2-hour lectures it took me to thoroughly cover this
material with a student who was mostly unfamiliar with graph theory.

<!--more-->

## Part 1

1. Set Theory Primer
2. Graph Terminology
3. Graph Representations
4. Breadth-first Search

### Set Theory Primer:

1.  set: collection of unique elements
2.  x \in set S
3.  x \notin set S
4.  Operations
    * intersection: create new set containing common elements of two other sets
    * union: create new set containing all [unique] elements from two other sets
    * difference: create new set with elements of 1st minus common elements of
      2nd
5.  disjoint: contain no common elements
6.  subset: contains some or all of the same elements as the superset
7.  proper subset: contains some but not all of the same elements as the superset
8.  empty set: contains no elements, represented by 0 symbol
9.  cardinality: size of the set; number of elements in the set
10. cartesian product (A X B) is the set of all ordered pairs such that the first
    element of the pair is an element of A and the second is an element of B

### Graph Terminology:

1.  vertex v \in V (you'll find me referring to these as nodes quite often)
2.  edge (u, v) \in E
3.  directed vs. undirected (each edge has a direction)
4.  weighted vs. unweighted
5.  bipartite graph
6.  source and sink (desination)
7.  in-degree and out-degree in directed graphs
8.  antiparallel in directed graphs (edge from u to v and edge from v to u)
9.  bipartite: graph whose vertices (V) can be divided into 2 disjoint sets,
    U = V - S and S (U, S) such that every edge connects a vertex in U to a
    vertex in S

### Graph Representations:

1.  adjacency list (good when \left\vert{E}\right\vert much <
    \left\vert{V}\right\vert^2)
     * undirected: size = 2\left\vert{E}\right\vert because each edge results in
       two entries
     * directed: size = \left\vert{E}\right\vert, (u,v) \in E represented by v
       in Adj[u] but not u in Adj[v]
        - u has edge to v but v does not have edge to u
2.  adjacency matrix (good for when \left\vert{E}\right\vert is close to
    \left\vert{V}\right\vert^2 = dense graph)

Typically stick with adj list because most graphs are sparse, rather than dense.

### Breadth-first Search (BFS):

1.  concept of discovery represented by colors:
    * white = undiscovered
    * gray = discovered and on the frontier of discovery
    * black = discovered and at least one layer back from the frontier (a vertex
      is only colored black once all adjacent vertices have been discovered)
2.  keeps track of distance (d) and predecessor (pi)
    * predecessor = parent of node (the node whose adjacency list was explored
      to get the current node)
3.  initialize by coloring all nodes white, setting d to infinity, and pi to nil
4.  move out from the source, traversing all edges at frontier layer to discover
    next layer
5.  upon discovering a white node, color it gray to mark it as discovered, set
    its predecessor to the node whose adj list it was fetched from, and set its
    distance to its predecessor's plus 1. Finally, add it to the Q.
6.  Once a node's adj list has been consumed, it is colored black
    then the next node is pulled from the Q and its adj list looped through
7.  Uses a queue to move through the list of nodes, with the main operations
    being a queue and a dequeue:
    * a node is dequeued, its adj list looped through, then colored black before
      moving on
    * each new node discovered is queued
    * this continues until the Q is finally empty

#### Time Complexity:

1.  queue/deqeueu is O(1), and happen once for every vertex, which gives a total
    of 2 * \left\vert{V}\right\vert = O(V)
2.  scans each adj list once, sum of all lengths of adj lists is
    2 * \left\vert{E}\right\vert = O(E)
3.  overhead for initialization involves a O(1) operation for each vertex = O(V)

**--> O(V) + O(V) + O(E) = O(V + E)**

#### Applications:

1. shortest path from a source s to a destination v
2. connected components
3. Ford-Fulkerson method

## Part 2

1. Depth-first search
2. Topological sort
3. Connected componenents
4. Dijkstra's algorithm

### Depth-first Search:

1.  same idea of colors to indicate discovery state
    * white = undiscovered
    * gray = discovered but not fully explored (on frontier)
    * black = discovered and adjacent vertices fully explored
2.  new attribute stored: 2 TIMESTAMPS for each vertex
    * each is int between 1 and 2\left\vert{V}\right\vert
    * v.d = discovery time
    * v.f = finishing time
    * note correspondence of colors: white before v.d, gray between v.d and
      v.f, and black after v.f
3.  don't store distance
4.  the specification is recursive (DFS-VISIT calls itself)
5.  first, initialize all vertices other than src to be white and have parent of
    null, then initialize the src to be gray and have a time of 1 & pi of null
6.  next, move through adj list of source using DFS-VISIT
7.  DFS-VISIT
    1. set time to be time + 1 and color to gray
    2. move down path recursively with DFS-VISIT
    3. once the call stack returns to the initial call, this vertex is colored
       black, finish time set to time + 1, and execution returns to next level
       up

#### Time Complexity:

1. Initialization: once for every vertex = O(V)
2. Distinct set of operations for every vertex = O(V)
3. Traversal for every edge in the graph = O(E)

**--> O(V + E)**

#### Applications:

1. Solving mazes
2. Topological sort
3. Connected components, strongly connected, cycles, bridges

### Connected Components:

1.  path = set of edges connecting two vertices
2.  connected component = subgraph in which any two vertices are connected by a
    path
3.  strongly connected component = every vertex is reachable from every other
    * this one applies exclusively to directed graphs
4.  cycle = sequence of vertices starting and ending at same vertex
5.  bridge = an edge whose deletion increases the number of connected components
    * a bridge connects 2 connected components; removing distinguishes them

### Topological Sort:

1.  DAG = directed acyclic graph (directed and no cycles)
    * often used to indicate precedences among events
2.  toplog sort gives us this ordering
    * Use DFS to compute finishing times v.f for each v \in G.V
    * add in step: when finished, insert onto front of linked list
    * afterwards, return the linked list.

#### Time Complexity:

1. Same as DFS, since we have only one additional operation for each vertex O(V)

**--> O(V + E)**

#### Applications:

1.  critical path
2.  valid ordering of events (dependency graph)

### Dijkstra's Algorithm:

1.  Problem description: find the single-source shortest path on a weighted,
    directed graph for the case in which all edge weights are nonnegative
2.  have w(u, v) >= 0 for each (u,v) \in E
3.  maintains set S of vertices whose final shortest-path weights have been
    calculated
    * for each we have some v.d value
    * have min priority Q keyed by v.d so the smallest v.d pops out first
4.  Steps:
    1. Initialization = set all v.d and v.pi values in normal way (think BFS)
    2. set S to empty set and Q to set G.V
    3. for each vertex in Q (G.V), in order of non-decreasing v.d, add to S and
       relax all adjacent edges

## Part 3

1. Flow Networks Terminology
2. Ford Fulkerson Method
3. Maximum Bipartite Graph
4. Min Cut Max Flow Theorem
5. Transforming Graphs into Flow Networks
6. Max Bipartite Matching

### Flow Networks Terminology:

Directed graph in which each edge has a nonnegative capacity c(u,v) >= 0

1.  If E contains an edge, there is no edge in opp direction
2.  source s has in-degree of 0
3.  sink t has out-degree of 0
4.  all nodes lie on path from s to t, so graph is connected
5.  Each vertex other than s has at least one entering edge, so
    \left\vert{E}\right\vert >= \left\vert{V}\right\vert - 1
6.  A flow is a function on a particular edge which satisfies 2 constraints
    1. capacity constraint: 0 <= f(u,v) <= c(u,v)
        * flow must not exceed capacity
        * flow must be nonnegative
    2. flow conservation: flow in equals flow out for u \in V - {s, t}
7.  Overall flow \left\vert{f}\right\vert of a network flow graph is \sum of all
    flows from s to t minus the \sum of all flows from t to s (important in
    residual graphs)
8.  all edges not shown are assumed to have capacity of 0 for ease of reasoning

### Ford Fulkerson Method:

Goal: find the max flow (f*)

Start with flow value of 0 and iteratively increase the value of the flow using
augmenting paths in residual network. Sometimes an augmentation may decrease
localized flows to increase the global flow

#### Terminology

1. Residual network (Gf)
   1. same V
   2. residual capacity = c(u,v) - f(u,v)
   3. edges from G in Gf only if residual capacity on that edge
   4. Gf also has an edge for each (u,v) with f(u,v) > 0
        * represented as (v,u) with cf(v,u) = f(u,v)
        * these represent a possible decrease in flow on that edge
   5. Each edge in Gf is either an edge in G or its reversal
        * \left\vert{Ef}\right\vert <= 2\left\vert{E}\right\vert
   6. Pushing flow on reverse edge is called cancellation
2. Augmenting path: a path from s to t in the residual network
    * these paths are guaranteed to increase overall \left\vert{f}\right\vert
      for G
3. Cut: partition V into 2 disjoint sets of vertices S and T
    * net flow f(S,T) across cut (S,T) is \sum of all flows from S to T
      minus \sum of all flows coming back from T to S (see p. 721)
    * capacity of cut is \sum of all capacities going from S to T
    * note the asymmetry

#### Algorithm Summary

1.  Set all flows to be 0 on all edges in G
2.  Construct residual graph Gf for G (DFS or BFS-->Edmonds-Karp)
3.  Find an augmenting path in Gf
4.  Update flow values for all edges in that path
5.  Repeat until no augmenting paths can be found

#### Time Complexity:

1.  While loop repeats no more than \left\vert{f*}\right\vert times (increase
    at least 1 each time)
2.  Using BFS or DFS for augmenting path discovery = O(V + E) per iteration
3.  Total this and you get O((V + E) * \left\vert{f*}\right\vert) which is
    linear
4.  Usually summarized to (E\left\vert{f*}\right\vert)
5.  When using BFS, this is reduced to O(VE^2)

**--> O(VE^2)**

#### Applications: General problem types:

1.  multi-source multi-sink max flow problem
2.  max cardinality bipartite matching
3.  max node-disjoint path
4.  max edge-disjoint path


### Max-flow Min-cut Theorem:

In a flow network, the following are equivalent:

1. f is a max flow in G
2. residual network Gf contains no augmenting paths
3. \left\vert{f}\right\vert = c(S,T) for some cut (S,T) of G

### Transforming Graphs into Flow Networks:

It is often necessary to alter the graph structure to meet the constraints of a
flow network. This is useful when the alterations are simple.

1.  antiparallel edges: introduce a new node between the two connected vertices
    to replace one of the edges. For instance, say we have (u,v). Introduce v'
    and two edges (u,v') and (v',v).
2.  multiple sources and sinks: introduce supersource s and supersink t
    * new edge from supersource to all existing sources
    * new edge from all existing sinks to supersink
    * all new edges given infinite capacity (should not limit current env)

### Max Bipartite Matching:

Find maximum number of matchings in a bipartite graph: network flow!

1.  matching: pairing of one item with another
    * one node in first set to another in 2nd
2.  perfect matching: all nodes in each set are matched
3.  Given a particular bipartite graph G = (V, E) with disjoint sets S and T:
    * introduce supersource s with edges to all nodes in S
    * introduce supersink t and make edges from all nodes in T to t
    * make all edges between nodes in S and nodes in T into directed edges
    * set all capacities to 1
    * find max flow: this is the optimal matching
    * if \left\vert{f*}\right\vert = \left\vert{S}\right\vert =
      \left\vert{T}\right\vert then it is a perfect matching

