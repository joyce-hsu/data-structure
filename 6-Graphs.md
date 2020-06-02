### Konigsberg Bridge Problem  

![konigsberg-bridge](https://github.com/joyce-hsu/data-structure/blob/master/konigsberg-bridge.png)  
![konigsberg-bridge2](https://github.com/joyce-hsu/data-structure/blob/master/konigsberg-bridge2.png)  
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
![graphs-sample](https://github.com/joyce-hsu/data-structure/blob/master/graphs-sample.png) 

**Graph Restrictions**  
- A graph may not have an edge from a vertex back to itself
  - (v, v) or <v, v> are called self edge or self loop.
  - 通常不會，但有時會:FSM(finite-state machine)(有限狀態機)
  - compiler檢查語法:利用graph-每個點(token)-利用FSM檢查-如果錯誤就看FSM停在哪裡
- A graph may not have multiple occurrences of the same edge
  - Without this restriction, it is called a multigraph.

![graphs-sample2](https://github.com/joyce-hsu/data-structure/blob/master/graphs-sample2.png)  
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
![subgraph](https://github.com/joyce-hsu/data-structure/blob/master/subgraph.png)  

**Graphs with Two Connected Components**
![connected-components](https://github.com/joyce-hsu/data-structure/blob/master/connected-components.png)  
Connected Components:表示任兩點都有連接，ex.4可以走到7  

**Strongly Connected Components of G3**  
![connected-components-strongly](https://github.com/joyce-hsu/data-structure/blob/master/connected-components-strongly.png)  
有方向性時會更嚴格
沒其他的頂點，是極端的例子(通常叫isolation point)  

---

### Degree of A Vertex  
- Degree of a vertex: The degree of a vertex is the number of edges incident to that vertex.
- If G is a directed graph, then we define
  - in-degree of a vertex: is the number of edges for which vertex is the head.
  - out-degree of a vertex: is the number of edges for which the vertex is the tail.
- For a graph G with n vertices and e edges, if di is the degree of a vertex i in G, then the number of edges of G is  ![degree-of-vertex](https://github.com/joyce-hsu/data-structure/blob/master/degree-of-vertex.png)  除以2是在無方向之下的例子  
  
**Abstract of Data Type Graphs**
````
class Graph
{
// objects: A nonempty set of vertices and a set of undirected edges
// where each edge is a pair of vertices
public:
    Graph(); // Create an empty graph
    void InsertVertex(Vertex v);
    void InsertEdge(Vertex u, Vertex v);
    void DeleteVertex(Vertex v);
    void DeleteEdge(Vertex u, Vertex v);
    
    Boolean IsEmpty(); // if graph has no vertices return TRUE
    
    List<List> Adjacent(Vertex v);
    // return a list of all vertices that are adjacent to v
};
````  
---
### Adjacency Matrix Representation
![adjacency-matrix](https://github.com/joyce-hsu/data-structure/blob/master/adjacency-matrix.png)  
頂點個數的平方  很花時間  

### Adjacency List Representation  
![adjacent-ists](https://github.com/joyce-hsu/data-structure/blob/master/adjacent-ists.png)  
![adjacent-ists2](https://github.com/joyce-hsu/data-structure/blob/master/adjacent-ists2.png)  

### Sequential Representation of Graph G4  
![sequential-representation-graph](https://github.com/joyce-hsu/data-structure/blob/master/sequential-representation-graph.png)  
0和誰有連接? index=0的地方存著9  代表要找index=9  可以看出0和1,2有連接  
第1~7格儲存查表位置  
因為是一為陣列，所以插入/刪去頂點時麻煩
**Inverse Adjacency Lists for G3**  
![inverse-adjacency-lists](https://github.com/joyce-hsu/data-structure/blob/master/inverse-adjacency-lists.png)  
看誰有連到某數  


### Multilists  
- In the adjacency-list representation of an undirected graph, each edge (u, v) is
represented by two entries.
- Multilists: To be able to determine the second entry for a particular edge and
mark that edge as having been examined, we use a structure called multilists.
  - Each edge is represented by one node.
  - Each node will be in two lists.  
  
![multilists](https://github.com/joyce-hsu/data-structure/blob/master/multilists.png)  
紅色N1 N2 和0有關的紀錄位置  
headnode1 2 3 4 表示頂點 指向第一次出現的位置  
N0~N5 edge的編號

**小總結**  
有四個表示法:  
1. matrix  
2. Adjacency List  
3. 1-D array  
4. multilist  
前三個同一個邊(u, v)在u被記錄,在v也被記錄  
multilist 以edge為主  (u, v)不被記錄兩次  
  
road network 的頂點是?  交叉路口即為一個頂點  

--
### Weighted Edges  
- Very often the edges of a graph have weights associated with them.
  - distance from one vertex to another
  - cost of going from one vertex to an adjacent vertex.
  - To represent weight, we need additional field, weight, in each entry.
  - A graph with weighted edges is called a network.

---
### Graph Operations  
- A general operation on a graph G is to visit all vertices in G that are reachable from a vertex v.
  - Depth-first search
  - Breath-first search  
  
**Depth-First Search 深度優先**  
- Depth First Search: generalization of preorder traversal
- Starting from vertex v, process v & then recursively traverse all vertices adjacent to v.
- To avoid cycles, mark visited vertex  
- Analysis of DFS
  - If G is represented by its adjacency lists, the DFS time complexity is O(e).
  - If G is represented by its adjacency matrix, then the time complexity to complete DFS is O(n2).  
![depth-first-search](https://github.com/joyce-hsu/data-structure/blob/master/depth-first-search.png)  
拜訪順序:0-1-3-7-4-5-2-6  
有一個boolean紀錄該數是否被output過  
用recursive跑不斷呼叫  
拜訪順序是否是唯一?  否，如果adjacency lists不同結果就會不同  
  
**Breath-First Search 廣度優先**  
- Breadth First search (BFS): level order tree traversal
- BFS algorithm: using queue
![breadth-first-search](https://github.com/joyce-hsu/data-structure/blob/master/breadth-first-search.png)  
拜訪A之後把BCD存在queue，然後因為沒有其他與A同深度的，故印出B  
印出B之後把C存進queue，接下來把D印出，同樣會讀取到C，但是C已經在queue中，就不重複存入  
接下來把E印出後，就印C了
