### Konigsberg Bridge Problem  

![konigsberg-bridge]()  
![konigsberg-bridge2]()  
B點degree=3 , A點degree=3  


給起始點，只能走過每座橋一次的情況下，有可能回到起點嗎?  
結論:degree of each vertex is even 的情況下可以  
vertex 是 A,B,C,D  

---

### Application of Graphs  
- Analysis of electrical circuits  :分析電路 layout
- Finding shortest routes  :地圖，找空間上、時間上的最短路徑
- Project planning  :開發流程
- Identification of chemical compounds
- Statistical mechanics
- Genertics
- Cybernetics
- Linguistics
- Social Sciences  :臉書的推薦好友  

---

### Definition of A Graph  
- A graph, G, consists of two sets, V and E.
  - V is a finite, nonempty set of vertices.
  - E is set of pairs of vertices called edges.
- The vertices of a graph G can be represented as V(G).
- Likewise, the edges of a graph, G, can be represented as E(G).
- Graphs can be either undirected graphs or directed graphs.
- For a undirected graph, a pair of vertices (u, v) or (v, u) represent the same edge.
- For a directed graph, a directed pair <u, v> has u as the tail and the v as the head. Therefore, <u, v> and <v, u> represent different edges.  
![graphs-sample]() 

**Graph Restrictions**  
- A graph may not have an edge from a vertex back to itself
  - (v, v) or <v, v> are called self edge or self loop.
  - 通常不會，但有時會:FSM(finite-state machine)(有限狀態機)
  - compiler檢查語法:利用graph-每個點(token)-利用FSM檢查-如果錯誤就看FSM停在哪裡
- A graph may not have multiple occurrences of the same edge
  - Without this restriction, it is called a multigraph.

![graphs-sample2]()  
(a)NLP(Natural Language Processing)檢查語法時可能會遇到  
(b)3號po文2號按讚多次發生把這些時間點記錄下來就有可能multigraph  

---
### Terminology of Graph  
- Graph: G=(V, E), V: a set of vertices, E: a set of edges
- Edge (arc): a pair (v,w), where v, w ∈ V
- Directed graph (Digraph): graph if pairs are ordered (directed edge)
- Adjacent: w is adjacent to v if (v,w) ∈ E
- Undirected graph: if (v,w) ∈ E, (v,w)=(w,v)
- Path: a sequence of vertices w1, w2, w3,…, wN where ( wi, wi+1) ∈ E, ∀ 1 ≤ i ≤ N.
- Length of a path: number of edges on the path.
- Simple path: a path where all vertices are distinct except the first and last.
- Cycle in a directed graph: a path such that w1 = wN
- Acyclic graph (DAG): a directed graph which has no cycles.
- Connected: an undirected graph if there is a path from every vertex to every vertex.
- Strongly connected: a directed graph if there is a path from every vertex to every vertex.
- Complete graph: a graph in which there is an edge between every pair of vertices.
  
**Complete Graph**  
- The number of distinct unordered pairs (u, v) with u≠v in a graph with n vertices is n(n-1)/2.
- A complete unordered graph is an unordered graph with exactly n(n-1)/2 edges.
- A complete directed graph is a directed graph with exactly n(n-1) edges.  
  
**Subgraphs**  
graph的子集合   
![subgraph]()  
