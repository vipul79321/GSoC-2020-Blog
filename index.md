***Student Name: Vipul Gupta***

***Organization: SageMath***

***Project Mentor: Dr. David Coudert***

***Project Title: Efficient methods for Diameter, Radius and All Eccentricities computations***

***Project URL: [https://summerofcode.withgoogle.com/projects/#4665936407166976](https://summerofcode.withgoogle.com/projects/#4665936407166976)***

---

## Organization Overview

SageMath is a free open-source mathematics software system licensed under the GPL. It builds on top of many existing open-source packages: NumPy, SciPy, matplotlib, Sympy, Maxima, GAP, FLINT, R and many more. Access their combined power through a common, Python-based language or directly via interfaces or wrappers. Along with that SageMath has its own implementation of various algorithms and methods, thereby increasing the overall functionality. SageMath has been actively participating in GSoC program since 2012.

---

## Project Overview

This project consists of two parts :

  * **Improving Diameter, Radius and All Eccentricities computation methods for (weighted) (di)graphs** - Previously, algorithms for Radius, Diameter, and All Eccentricities computation were too slow in practice. They were based on computing eccentricity of each vertex using shortest paths (all pairs or single source) method. Although for diameter calculation, there are 2Sweep, MultiSweep, and iFUB algorithms, which are somewhat fast. But all three of them were restricted to unweighted and undirected graphs. In this part, we completed the implementation of best-known algorithms of the above purposes for (weighted) (di)graphs. Although, the worst case time complexity of these algorithms are still the same as previous ones, but they are much faster in practice. See this for example - 
  
  ```
  sage: G = graphs.RandomGNP(1000, 0.6)
  sage: %time G.radius(algorithm = 'BFS')  // previous scenario
  CPU times: user 2min 9s, sys: 26 s, total: 2min 35s
  Wall time: 2min 35s
  2
  sage: %time G.radius(algorithm = 'DHV')  // current scenario
  CPU times: user 181 ms, sys: 7.99 ms, total: 189 ms
  Wall time: 188 ms
  2
  ```

  * **Refactoring and improving distance computation methods** - In this part, we optimized certain distances related methods. For example, reduced the space complexity of the methods such as Wiener Index, Distances Distribution. Improved the overall consistency of weight_function throughout the graph module. Also, fixed minor bugs in the shortest path methods. 
  
---

## Getting Started

I was already familiar with Github. But SageMath's development takes place on [Trac](https://trac.sagemath.org/) server. So, I followed [SageMath's developer guide](https://doc.sagemath.org/html/en/developer/index.html) to setup and get myself familiar with trac server. To have a hands-on experience in SageMath's development, I started by contributing to the open tickets which were pending for a long-time. Few of them are mentioned below - 

  * [#19053](https://trac.sagemath.org/ticket/19053) - This ticket aimed at implementing arboricity method for undirected graphs, which is a measure of how dense a graph is, using Matroid partitioning algorithm. It was pending for five years. I completed it by doing some changes and adding more doc-tests.
  
  * [#23115](https://trac.sagemath.org/ticket/23115) - This ticket was pending for three years. I completed it by implementing Out-branching and In-branchings method for Directed graph, which can also be used to generate spanning in/out branching of that graph.
  
  * [#21423](https://trac.sagemath.org/ticket/21423) - This ticket aimed at adding Cube-Connected Cycle generator in Families of graphs.
  
  * [#29275](https://trac.sagemath.org/ticket/29275) - I created this ticket to make from_oriented_incidence_matrix method in graph_input.py able to handle incidence matrix with only two rows.
  
  * [#29276](https://trac.sagemath.org/ticket/29276) - Similar to [#29275](https://trac.sagemath.org/ticket/29275), this ticket fixed the case of all zero entries in a column of incidence matrix by returning a loop-less version of that graph.
  
  * [#29351](https://trac.sagemath.org/ticket/29351) - I created this ticket to implement a directed versionof 2sweep algorithm for lower bound of diameter computation in directed graphs.
  
----
  
## Community Bonding Period

This period involved discussing layout for the project and deciding locations for each method inside the Graph module. Also, organizing radius, diameter, and eccentricity computation method separately for undirected and directed graphs in graph.py and digraph.py respectively.

Related Ticket - [#29660](https://trac.sagemath.org/ticket/29660)

----

## Phase - I

1). Implemented **Radius** computation methods for **(weighted) undirected graphs** proposed in <span id="a1">[[1]](#f1)</span>.

   Related ticket : [#29715](https://trac.sagemath.org/ticket/29715)
#### Pseudo-Code

   <script src="https://gist.github.com/vipul79321/1200671915391cfea1ebe991e6c332c9.js"></script>
   
<br>

2). Implemented **Diameter** computation for **(weighted) undirected graphs** proposed in <span id="a1">[[1]](#f1)</span>.

   Related ticket : [#29744](https://trac.sagemath.org/ticket/29744)
#### Pseudo-Code

   <script src="https://gist.github.com/vipul79321/ccd900ba4bf0b4d77abd70f4dc15a1b8.js"></script>

<br>

3). Implemented **All eccentricities** computation methods for **(weighted) undirected graphs** proposed in <span id="a1">[[1]](#f1)</span>.

  Related ticket : [#27934](https://trac.sagemath.org/ticket/27934)
#### Pseudo-Code

  <script src="https://gist.github.com/vipul79321/7c7c38ae21b05b55d9dae14e131d7629.js"></script>

<br>

4). Fixed a small bug in **shortest_path_length** method in generic_graph.py.
  
  Related ticket: [#29734](https://trac.sagemath.org/ticket/29734)

----

## Phase - II

  1). Implemented weighted version of **2Dsweep** method for computation of lower bound on the diameter of weighted directed graphs given in <span id="a2">[[2]](#f2)</span> and implemented **DiFUB (Directed iterative Finge Upper Bound)** method for exact computation of diameter of (weighted) directed graphs proposed in <span id="a3">[[3]](#f3)</span>.

  Related ticket : [#29422](https://trac.sagemath.org/ticket/29422), [#30039](https://trac.sagemath.org/ticket/30039)
#### Pseudo-Code for DiFUB

  <script src="https://gist.github.com/vipul79321/b9ef00a36c9f5dfa73d607eaba99edfb.js"></script>

<br>

2). Improved overall consistency and documentation in usage of **weight_function** in graph module.

  Related ticket : [#30081](https://trac.sagemath.org/ticket/30081)

----

## Phase - III

1). Completed memory efficient implementation of **wiener index** for (weighted) (di)graphs by avoiding to compute and store into memory the full distance matrix. This way we can compute this index for larger graphs.

  Related ticket : [#30247](https://trac.sagemath.org/ticket/30247)

2). Improved space usage in computation of **distances_distribution** of unweighted (di)graphs from `O(n^2)` to `O(n)` by avoiding to compute and store into memory the full distance matrix.

  Related ticket : [#30269](https://trac.sagemath.org/ticket/30269)

----

## Acknowledgement

First and foremost, I would like to express my sincere gratitude towards Dr. David Coudert, for his dedicated guidance and encouragement throughout the GSoC and prior to it, when I was learning SageMath development. He was very understanding and supportive of the fact that the student might have other academic commitments. He even helped me in optimizing some algorithms and encouraged me to see the bigger picture. Every discussion with him improved my understanding of the project. I have become a lot better at writing clean and efficient codes in Python. Working with SageMath over the summer was a great learning experience and has enhanced my passion for open source. I certainly want to contribute more to open source libraries, and I plan to continue working with SageMath.

And most importantly, I would also like to thank the people behind Google Summer of Code. I had a delightful experience working in GSoC 2020.

----

## References

1. <span id="f1"></span> [Feodor Dragan, Michel Habib, Laurent Viennot. “Revisiting Radius, Diameter, and all Eccentricity Computation in Graphs through Certificates”.](http://arxiv.org/abs/1803.04660) [↩](#a1)

2. <span id="f2"></span> [Broder, A.Z., Kumar, R., Maghoul, F., Raghavan, P., Rajagopalan, S., Stata, R., Tomkins, A., Wiener, J.L.: Graph structure in the web. Computer Networks 33(1-6), 309–320 (2000)](https://doi.org/10.1145/1412228.1455266) [↩](#a2)

3. <span id="f3"></span> [Pierluigi Crescenzi, Roberto Grossi, Leonardo Lanzi, and Andrea Marino.“On computing the diameter of real-world directed (weighted) graphs”. In Proceedings of the 11th International Symposium on Experimental Algorithms(SEA), pages 99–110, 2012.](https://doi.org/10.1007/978-3-642-30850-5_10) [↩](#a3)



```c++
int main()
{ 
    int x;
    cin>>x;
    return 0;
}
```
