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
右:complete binary tree  
  
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
> Let n and B denote the total number of nodes & branches in T. (n:節點數;B:pointer數)
root沒有人指,所以B = n-1
Let n0, n1, n2 represent the nodes with no children, single child, and two children respectively.  
n= n0+n1+n2, B+1=n, B=n1+2n2 ==> n1+2n2+1=n  
n1+2n2+1= n0+n1+n2 ==> n0=n2+1
![relations-between-Leaf-and-Degree2]()  

**Full BT VS Complete BT**  
- Full BT  
A full binary tree of depth k is a binary tree of depth k having 2^k -1 nodes, k>=0.
除了終端節點外，每個node都要有兩個pointer  
- Complete BT  
A binary tree with n nodes and depth k is complete iff its nodes correspond to the nodes numbered from 1 to n in the full binary tree of depth k.  
當我們有n個node，這n個node都要在Full Binary Tree的前十個位置  
![full-complete-BT]()  

老師問:如果H,I移到G下面，是否為complete BT?  
答:Nooooooo\~~~~~~~~  這樣前面就缺角了  

[參考資料](http://alrightchiu.github.io/SecondRound/binary-tree-introjian-jie.html)  

**Array Representation of A Binary Tree**  
1. If a complete binary tree with n nodes is represented sequentially, then for any node with index i, 1 ≤ i ≤ n, we have:
– parent(i) is at *i/2* if i ≠1. If i = 1, i is at the root and has no parent.
– left_child(i) is at *2i* if 2i ≤ n. If 2i > n, then i has no left child.
– right_child(i) is at *2i + 1* if 2i + 1 ≤ n. If 2i + 1 > n, then i has no right child.
2. Position zero of the array is not used.  
![sequential-representation]()   
找親代或子代很方便
缺點: 缺節點時會造成空間浪費、插入或刪除節點會需要進行資料搬移  

**Compare two binary tree representations**  
![compare-two-BT]()

---

### Node Representation  
![Node Representation]()  

**Linked Representation**  
````
class Tree;
class TreeNode {
    friend class Tree;
    private:
        TreeNode *LeftChild;
        char data;
        TreeNode *RightChild;
    };
class Tree {
    public:
    // Tree operations
    .
    private:
        TreeNode *root;
};
````
**Linked List Representation For The Binary Trees**  
![linked-list-representation-BT]()  
左:skewed binary tree 歪斜二元樹  
右:complete binary tree  

---

###Binary Tree Traversals  
- Let L, V, and R stand for moving left, visiting the node, and moving right.
- There are six possible combinations of traversal
  – LVR, LRV, VLR, VRL, RVL, RLV
- Adopt convention that we traverse left before right, only 3 traversals remain
  – LVR, LRV, VLR
  – inorder, postorder, preorder  
  
**老師問**  
為什麼要走訪(Traversal)?  
1. 印出來變成string，再比較string就可以知道兩個tree是否一樣  
2. copy tree會用到  

**Arithmetic Expression Using BT**  
![arithmetic-expression]()  

**Trace Operations of Inorder Traversal**  
![inorder-traversal]()  
  
Program 5.1 : inorder
````
void Tree::inorder()
// Driver calls workhorse for traversal of entire tree. The
// driver is declared as a public member function of Tree.
{
inorder(root);
}
void Tree::inorder(TreeNode *CurrentNode)
// Workhorse traverses the subtree rooted at CurrentNode (
// which is a pointer to a node in a binary tree). The workhorse
// is declared as a private member function of Tree.
{
    if(CurrentNode){
        inorder(CurrentNode -> LeftChild);  //L
        cout << CurrentNode -> data;        //V
        inorder(CurrentNode-> RightChild);  //R
    }
}
````
Program 5.2 : preorder
````
void Tree::preorder(){
// Driver calls workhorse for traversal of entire tree. The
// driver is declared as a public member function of Tree.
preorder(root);
}
void Tree::preorder(TreeNode *CurrentNode)
// Workhorse traverses the subtree rooted at CurrentNode (
// which is a pointer to a node in a binary tree). The workhorse
// is declared as a private member function of Tree.
{
    if(CurrentNode){
        cout << CurrentNode -> data;         //V
        preorder(CurrentNode -> LeftChild);  //L
        preorder(CurrentNode-> RightChild);  //R
    }
}
````
Program 5.3 : postorder  
````
void Tree::postorder()
// Driver calls workhorse for traversal of entire tree. The
// driver is declared as a public member function of Tree.
{
postorder(root);
}
void Tree::postorder(TreeNode *CurrentNode)
// Workhorse traverses the subtree rooted at CurrentNode (
// which is a pointer to a node in a binary tree). The workhorse
// is declared as a private member function of Tree.
{
    if(CurrentNode){
        postorder(CurrentNode -> LeftChild);  //L
        postorder(CurrentNode-> RightChild);  //R
        cout << CurrentNode -> data;          //V
    }
}
````
以上三個是recursive function  

**Iterative Inorder Traversal**  
用非遞迴的方式處理   

````
void Tree::NonrecInorder()
// nonrecursive inorder traversal using a stack
{
    Stack<TreeNode *> s; // declare and initialize stack
    TreeNode *CurrentNode = root;
    while (1) {
        while (CurrentNode) { // move down LeftChild fields
            s.Add(CurrentNode); // add to stack
            CurrentNode = CurrentNode->LeftChild;
        }
    if (!s.IsEmpty()) { // stack is not empty
        CurrentNode = *s.Delete(CurrentNode);
        cout << CurrentNode->data << endl;
        CurrentNode = CurrentNode->RightChild;
    }
    else break;
    }
}
````  
**老師問**
如果preorder/postorder要用nonrecursive...如何做?  
