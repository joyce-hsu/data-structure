### Trees  
Tree: a collection of nodes  
– a distinguished node r (root)
– zero or more nonempty (sub)trees  
tree的應用很廣: PSC:node即是基地台  
  
**Terminology**  
!(sample-tree)[]  
- level 表示這個tree有幾層  
The height or the depth of a tree is the maximum level of any node in the tree.  
- degree 表示有多少pointer  
- The node with degree 0 is a leaf or terminal node.(終端節點)
- A node that has subtrees is the parent of the roots of the subtrees.(親代)
- The roots of these subtrees are the children of the node.(子代)
- Children of the same parent are siblings.
- The ancestors of a node are all the nodes along the path from the root to the node.  
  
**List Representation**
( A ( B ( E ( K, L ), F ), C ( G ), D ( H ( M ), I, J ) ) )  
The root comes first, followed by a list of sub-trees  
![list-representation]()  

**Possible Node Structure For A Tree of Degree**  
Lemma 5.1:   
If T is a k-ary tree (i.e., a tree of degree k) with n nodes,   
each having a fixed size as in Figure 5.4,   
then n(k-1) + 1 of the nk child fileds are 0, n ≥ 1.
(k-ary tree: binary tree(B tree) k = 2)  
![Figure-5.4]()  
浪費、沒用到的pointer數量為: nk-(n-1)=n(k-1)+1  

**Left Child-Right Sibling Representation**  
Each node has two links (or pointers).  
Each node only has one leftmost child and one closest sibling.  
![left-child-right-sibling]()  
  
---
  
**Degree Two Tree Representation - Binary Tree**  
![binary-tree]()  
  
![distinctions-between-binarytree-and-tree]()
- There is no tree with zero nodes. But there is an empty binary tree.
- Binary tree distinguishes between the order of the children while in a tree we do not.
有分左跟右  

**Binary Tree Example**  
![binary tree example]()  
左:skewed binary tree 歪斜二元樹  
右:complete binary tree 完滿二元樹  
  
**The Properties of Binary Trees**  
  
**Maximum Number of Nodes in BT**  
Lemma 5.2 \[Maximum number of nodes]  
1. The maximum number of nodes on level i of a binary tree is 2^(i-1), i ≥ 1.  
2. The maximum number of nodes in a binary tree of depth k is 2^k – 1, k ≥ 1.  
![maximum-number-nodes-BT]()  
![maximum-number-nodes-BT-2]()  

**Relations between Number of Leaf Nodes and Nodes of Degree 2**  
For any nonempty binary tree, T, if n0 is the number of leaf nodes and n2 the number of nodes of degree 2, then n0=n2+1  
proof:
> Let n and B denote the total number of nodes & branches in T.  
Let n0, n1, n2 represent the nodes with no children, single child, and two children respectively.  
n= n0+n1+n2, B+1=n, B=n1+2n2 ==> n1+2n2+1= n
n1+2n2+1= n0+n1+n2 ==> n0=n2+1
