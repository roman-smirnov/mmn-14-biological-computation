# MMN 14 - Biological Computation 



## Question 1.A 

Given a graph of N vertices, if we suppose the graph is complete then the problem is equivalent to ordering N items without redraw. Therefore, by way of well known combinatorial considerations, there are N! possible orderings. If the graph is not complete, than some possibilities are not valid and no new ordering are made possible. 

We conclude that there are at-most N! possibilities. 

## Question 1.B

Let's analyze the time complexity of each step in the algorithm:

1. Generate all possibilities. 

   A chemical reaction which is performed over the input in parallel and is indepenent of the input size - O(1) (😊).

2. same as 😊

3. same as 😊

4. Extraction of paths which visit all vetices. 

   This step performs as many actions as there are vertices in the input. Therefore, its time complexity is linear - O(n).

5. same as 😊

6. same as 😊

By way of the above and complexity algebra, the overall time complexcity of the algorithm is O(n).

## Question 2

__Disclaimer__: couldn't figure this out on my own. Used a paper as a reference: _DNA Solution of the Maximal Clique Problem_, by Qi Ouyang,* Peter D. Kaplan, Shumao Liu, Albert Libchaber. Dated 23 June 1997.

### Definitions

_Graph_: a simple, undirected graph.

_Complete Graph_: a graph with an edge between every pair of vertices.

_Complementary Graph_: a graph constructed of the same set of vertices as the original graph, such that its set of edges is composed of all possible edges which do not appear in the original graph. 

_Clique_: a set of vertices belonging to a complete sub-graph.

_Invalid Clique_: a clique which contains a pair of vertices not connected by an edge (alternatively, are connected by an edge in the complementary graph).

_Max Clique_:  a set of vertices belonging to the largest (vertex wise) complete sub-graph. For a graph with N vertices, a max clique will have at most N vertices and at least 0 vertices. 

### Algorithm Overview

#### Encoding

Given a graph of N vertices, we enumerate and then encode the vertices into a N digit binary number, such that each digit correspond to the presence (1) or absence (0) of a vertex in a clique. The binary number with the mosts 1s which encodes a valid clique represents the max clique. 

#### Formulation

1. Generate the complementary graph.
2. Generate a set of all possible N digit binary numbers.
3. By way of the complementary graph, eliminate all binary numbers which represent an invalid clique.
4. Sort the numbers in the filtered set, by their count of 1s, into an ordered set.
5. Extract the binary number with the most 1s. 

### Algorithm Implementation

#### DNA Representation

The binary number is represented by a double stranded DNA sequence. Every binary digit $i$ is represented by an arbitrary generated position sequence $P_i$ followed by a value sequence $V_i$, and the next position sequence $P_{i+1}$. If $i=1$ then the length of $V_i$ is 0, else if $i=0$ then $V_i$ is represented by a sequence of some pre-defined length.

Each $V_i$ where $i=1$ contains a target sequence for a restriction enzyme ( a concatanation of part of $P_i$ and $P_{i+1}$ ).

#### Execution Steps

1. Insert multiple copies of all value and position sequences with their complement extension sequences into a Lygase solution. The process will generate all possible sequences $P_0 V_0 … P_n V_n P_{n+1}$.
2. Divide the solution into two equal parts.
3. Apply restriction enzymes to break down sequences which represent vertices having a common edge in the complementary graph. Break down a different edge vertex sequence in each part of the solution to eliminate sequences containing both vertices. This is done via the restriction enzyme targets encoded into each $V_i$. 
4. Recombine into a single solution. 
5. Exponentially multiply by way of polymerase chain reaction with primers targeting sequences having both a $P_0$ and a $P_{n+1}$ sequence sections (i.e were not broken by a restriction enzyme).
6. Repeat steps 2-5 for every edge in the complementary graph. 
7. Apply Gel Electrophoresis to sort double stranded sequences by length.
8. Shortest sequence will be a representation of a binary encoded max clique. 