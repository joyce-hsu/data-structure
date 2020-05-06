### Trees  
Tree: a collection of nodes  
– a distinguished node r (root)
– zero or more nonempty (sub)trees  
tree的應用很廣: PSC:node即是基地台  
  
**Terminology**  
![sample-tree](https://github.com/joyce-hsu/data-structure/blob/master/sample-tree.png)  
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
![list-representation](https://github.com/joyce-hsu/data-structure/blob/master/list-representation.png)  

**Possible Node Structure For A Tree of Degree**  
Lemma 5.1:   
If T is a k-ary tree (i.e., a tree of degree k) with n nodes,   
each having a fixed size as in Figure 5.4,   
then n(k-1) + 1 of the nk child fileds are 0, n ≥ 1.
(k-ary tree: binary tree(B tree) k = 2)  
![Figure-5.4](https://github.com/joyce-hsu/data-structure/blob/master/figure-5.4.png)  
浪費、沒用到的pointer數量為: nk-(n-1)=n(k-1)+1  

**Left Child-Right Sibling Representation**  
Each node has two links (or pointers).  
Each node only has one leftmost child and one closest sibling.  
![left-child-right-sibling](https://github.com/joyce-hsu/data-structure/blob/master/left-child-right-sibling.png)  
  
---
  
### Degree Two Tree Representation - Binary Tree**  
![binary-tree](https://github.com/joyce-hsu/data-structure/blob/master/binary-tree.png)  
  
**Distinctions between a binary tree and a tree**  
![distinctions-between-binarytree-and-tree](https://github.com/joyce-hsu/data-structure/blob/master/distinctions-between-binarytree-and-tree.png)
- There is no tree with zero nodes. But there is an empty binary tree.
- Binary tree distinguishes between the order of the children while in a tree we do not.
有分左跟右  

**Binary Tree Example**  
![binary tree example](https://github.com/joyce-hsu/data-structure/blob/master/binary-tree-example.png)  
左:skewed binary tree 歪斜二元樹  
右:complete binary tree  
  
**The Properties of Binary Trees**  
  
**Maximum Number of Nodes in BT**  
Lemma 5.2 \[Maximum number of nodes]  
1. The maximum number of nodes on level i of a binary tree is 2^(i-1), i ≥ 1.  
2. The maximum number of nodes in a binary tree of depth k is 2^k – 1, k ≥ 1.  
![maximum-number-nodes-BT](https://github.com/joyce-hsu/data-structure/blob/master/maximum-number-nodes-BT.png)  
![maximum-number-nodes-BT-2](https://github.com/joyce-hsu/data-structure/blob/master/maximum-number-nodes-BT-2.png)  

**Relations between Number of Leaf Nodes and Nodes of Degree 2**  
For any nonempty binary tree, T, if n0 is the number of leaf nodes and n2 the number of nodes of degree 2, then n0=n2+1  
proof:
> Let n and B denote the total number of nodes & branches in T. (n:節點數;B:pointer數)
root沒有人指,所以B = n-1
Let n0, n1, n2 represent the nodes with no children, single child, and two children respectively.  
n= n0+n1+n2, B+1=n, B=n1+2n2 ==> n1+2n2+1=n  
n1+2n2+1= n0+n1+n2 ==> n0=n2+1
![relations-between-Leaf-and-Degree2](https://github.com/joyce-hsu/data-structure/blob/master/relations-between-Leaf-and-Degree2.png)  

**Full BT VS Complete BT**  
- Full BT  
A full binary tree of depth k is a binary tree of depth k having 2^k -1 nodes, k>=0.
除了終端節點外，每個node都要有兩個pointer  
- Complete BT  
A binary tree with n nodes and depth k is complete iff its nodes correspond to the nodes numbered from 1 to n in the full binary tree of depth k.  
當我們有n個node，這n個node都要在Full Binary Tree的前十個位置  
![full-complete-BT](https://github.com/joyce-hsu/data-structure/blob/master/full-complete-BT.png)  

老師問:如果H,I移到G下面，是否為complete BT?  
答:Nooooooo\~~~~~~~~  這樣前面就缺角了  

[參考資料](http://alrightchiu.github.io/SecondRound/binary-tree-introjian-jie.html)  

**Array Representation of A Binary Tree**  
1. If a complete binary tree with n nodes is represented sequentially, then for any node with index i, 1 ≤ i ≤ n, we have:
– parent(i) is at *i/2* if i ≠1. If i = 1, i is at the root and has no parent.
– left_child(i) is at *2i* if 2i ≤ n. If 2i > n, then i has no left child.
– right_child(i) is at *2i + 1* if 2i + 1 ≤ n. If 2i + 1 > n, then i has no right child.
2. Position zero of the array is not used.  
![sequential-representation](https://github.com/joyce-hsu/data-structure/blob/master/sequential-representation.png)   
找親代或子代很方便
缺點: 缺節點時會造成空間浪費、插入或刪除節點會需要進行資料搬移  

**Compare two binary tree representations**  
![compare-two-BT](https://github.com/joyce-hsu/data-structure/blob/master/compare-two-BT.png)

---

### Node Representation  
![Node Representation](https://github.com/joyce-hsu/data-structure/blob/master/node-representation.png)  

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
![linked-list-representation-BT](https://github.com/joyce-hsu/data-structure/blob/master/linked-list-representation-BT.png)  
左:skewed binary tree 歪斜二元樹  
右:complete binary tree  

---

### Binary Tree Traversals  
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
![arithmetic-expression](https://github.com/joyce-hsu/data-structure/blob/master/arithmetic-expression.png)  

**Trace Operations of Inorder Traversal**  
![inorder-traversal](https://github.com/joyce-hsu/data-structure/blob/master/inorder-traversal.png)  
  
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

**Level-Order Traversal**  
- All previous mentioned schemes use stacks
- Level-order traversal uses a queue
- Level-order scheme visits the root first, then the root’s left child, followed by the root’s right child
- All the nodes at a level are visited before moving down to another level
  
**Level-Order Traversal of A Binary Tree**  
````
void Tree::LevelOrder()
// Traverse the binary tree in level order
{
    Queue<TreeNode *> q;
    TreeNode *CurrentNode = root;
    while (CurrentNode) {
        cout << CurrentNode->data<<endl;
        if (CurrentNode->LeftChild) q.Add(CurrentNode->LeftChild);
        if (CurrentNode->RightChild) q.Add(CurrentNode->RightChild);
        CurrentNode = *q.Delete();
    }
}
````
queue有FIFO的特性，所以加入queue的順序不能亂改  

---

**Some Other Binary Tree Functions**  
With the inorder, postorder, or preorder mechanisms, we can implement all needed binary tree functions. e.g.,  
 - Copying Binary Trees  
 - Testing Equality  
   - Two binary trees are equal if their topologies are the same and the information in corresponding nodes is identical.  
  
Program 5.9: **Copy constructor**  
````
Tree::Tree(const Tree& s) //driver
{
    root = copy(s.root);
}
TreeNode* Tree::copy(TreeNode *orignode) //Workhorse
//This function returns a pointer to an exact copy of the binary
//tree rooted at orignode.
{
    if(orignode) {
        TreeNode *temp = new TreeNode;
        temp->data = orignode->data;  //V
        temp->LeftChild = copy(orignode->LeftChild); //L
        temp->RightChild = copy(orignode->RightChild);  //R
        return temp;
    }
    else return 0;
}
````  
temp->LeftChild = copy(orignode->LeftChild); 是recursive!!  
倒數第五到七行很像VLR preorder!!  
**老師問:** 可以用inorder/postorder來cory tree嗎?  
我的想法:可以!有每個走到就行(?)  

Program 5.10: **Driver-assumed to be a friend of class Tree.**  
````
int operator==(const Tree& s, const Tree& t)
{
    return equal(s.root, t.root);
}
//Workhorse-assumed to be a friend of TreeNode.
int equal(TreeNode *a, TreeNode *b)
//This function returns 0 if the subtrees at a and b are not
//equivalent. Otherwise, it will return 1.
{
    if((!a)&&(!b)) return 1; //both a and b are 0
        if(a && b //both a and b are non-0
            && (a->data == b->data) //data is the same
            && equal(a->LeftChild, b->LeftChild)
            //left subtrees are the same
            && equal(a->RightChild, b->RightChild))
            //right subtrees are the same
        return 1;
    return 0;
}
````  
中間的 if 判斷很長!但是確認是否為相同的樹還算容易  
如果要判對是否為相似的樹，就要看定義來寫判斷，判斷有可能會更長  

---

**Propositional Calculus Expression**  
- variable is an expression.
- If x and y are expressions, then ¬x, x∧y, x∨y are expressions.
- Parentheses can be used to alter the normal order of evaluation (¬ > ∧ > ∨).
- Example: x1 ∨ (x2 ∧ ¬x3)
- Satisfiability problem: is there an assignment to make an expression true?  
![calculus-expression](https://github.com/joyce-hsu/data-structure/blob/master/calculus-expression.png)  
自己看書:如何建出這棵樹的?  

**Perform Formula Evaluation**  
- To evaluate an expression, we can traverse its tree in postorder.  
- To perform evaluation, assume that each node has four fields  
  - LeftChild  
  - data 用來存T/F, ∨(or) , ∧(and) , ¬(not)   
  - value 用來存判斷的結果  
  - RightChild  
  
**First Version of Satisfiability Algorithm**  
````
For all 2n possible truth value combinations for the n
variables
{
    generate the next combination;
    replace the variables by their values;
    evaluate the formula by traversing the tree it points to
    in postorder;
    if (formula.rootvalue()) {cout << combination; return;}
}
Cout << “no satisfiable combination”;
````

**Evaluating A Formula**  
````
void SatTree::PostOrderEval() // Driver
{
    PostOrderEval(root);
}
void SatTree::PostOrderEval(SatNode * s) // workhorse
{
    if (s) {
        PostOrderEval(s->LeftChild);
        PostOrderEval(s->RightChild);
        switch (s->data) {
            case LogicalNot: s->value =!s->RightChild->value;
                break;
            case LogicalAnd: s->value = s->LeftChild->value && s->RightChild->value;
                break;
            case LogicalOr: s->value = s->LeftChild->value || s->RightChild->value;
                break;
            case LogicalTrue: s->value = TRUE; break;
            case LogicalFalse: s->value = FALSE; break;
        }
    }
}
````  

在stack&queue的時候有算過四則運算  
當時有兩個phase:
- phase 1: infix 轉換成 postfix
- phase 2: 將postfix加入stack，如果是數字直接add，遇到operator把最上面兩個數字取出，運算後放回stack  
  
現在也是兩個phase
- 建出這棵樹
- 利用樹來儲存與判斷結果，最後的結果會放在root  
![calculus-expression2](https://github.com/joyce-hsu/data-structure/blob/master/calculus-expression2.png) 

**老師問:** 想想看如何用樹來計算四則運算?
  
---

### Threaded Binary Tree  
讓沒有用到的link充分利用  
Too many null pointers in current representation of binary trees  
n: number of nodes  
number of non-null links: n-1 (每個node都有被指到,除了root之外)  
total links: 2n (每個node下面有兩個link)   
null links: 2n-(n-1)=n+1  
  
Replace these null pointers with some useful “threads”  

![threaded-BT](https://github.com/joyce-hsu/data-structure/blob/master/threaded-BT.png)  
虛線是threaded  
- If ptr->left_child is null, replace it with a pointer to the node that would be visited before ptr in an inorder traversal  
- If ptr->right_child is null, replace it with a pointer to the node that would be
visited after ptr in an inorder traversal  
  
如此一來需要判斷是tree pointer或是 threaded  
To distinguish between normal pointers and threads, two boolean fields, LeftThread and RightThread, are added to the record in memory representation.  
- t->LeftThread = TRUE => t->LeftChild is a thread.  
- t->LeftThread = FALSE => t->LeftChild is a pointer to the left child.  
![threaded](https://github.com/joyce-hsu/data-structure/blob/master/threaded.png)  
  
To avoid dangling threads, a head node is used in representing a binary tree.  
The original tree becomes the left subtree of the head node.  
![figure-5.20](https://github.com/joyce-hsu/data-structure/blob/master/figure-5.20.png)   
包含head node的 LEVEL 4 其中的 E 少一條threaded ; F 兩側的f都應標示成t  
   
![threaded-code](https://github.com/joyce-hsu/data-structure/blob/master/threaded-code.png)  
老師說可能是他code打得少，目前也還沒使用過Threaded Binary Tree (哈哈)  
使用Threaded Binary Tree雖然利用了原本是NULL的地方  
卻也增加了兩個欄位在insert/delete也要更多的Ppointer assignment  
  
**Insertion of r As a Right Child of s in A Threaded Binary Tree**  
![threaded-insertion](https://github.com/joyce-hsu/data-structure/blob/master/threaded-insertion.png)  
![threaded-insertion2](https://github.com/joyce-hsu/data-structure/blob/master/threaded-insertion2.png)  

````
void ThreadedTree::InsertRight(ThreadNode *s, ThreadedNode *r)
// Insert r as the right child of s
{
    r->RightChild = s->RightChild;
    r->RightThread = s->RightThread;
    r->LeftChild = s;
    r->LeftThread = TRUE; // LeftChild is a thread
    s->RightChild = r; // attach r to s
    s->RightThread = FALSE;
    if (!r->RightThread) {
        ThreadedNode *temp = InorderSucc(r); // returns the inorder successor of r
        temp->LeftChild = r;
    }
}
````

---

### Huffman Codes  
我們要將整篇文章編碼，事先將頻繁使用的word記錄下來，並讓頻繁字詞使用最少單位的碼(code size小)  
如此一來解碼比較快  

The expected decoding time is minimized by choosing code words resulting in a decode tree with minimal weighted external path length.  
![decode-tree](https://github.com/joyce-hsu/data-structure/blob/master/decode-tree.png)  
最靠近root的字詞M4最常使用，在此樹狀圖中M4的編碼為 1    
M1 = 000 ; M2 = 001 ; M3 = 01  
最頻繁使用的字詞編碼最短，而較少使用的字編碼長一些較不會影響解碼時間  
  
![huffman-tree-example](https://github.com/joyce-hsu/data-structure/blob/master/huffman-tree-example.png)  
長方形框框中的數字代表該字詞的使用頻率  
a. 將使用頻率最小的兩個merge變成一顆tree，parent變成他們頻率的總和  
b. 將使用頻率最小的兩個merge變成一顆tree，剛剛合成出的 5 還是最小的兩個之一，所以又被merge  
以此類推......  
  
**Huffman Function**  
````
class BinaryTree {
public:
    BinaryTree(BinaryTree bt1, BinaryTree bt2) {
        root->LeftChild = bt1.root;
        root->RightChild = bt2.root;
        root->weight = bt1.root->weight + bt2.root->weight;
    }
private:
    BinaryTreeNode *root;
}

void huffman (List<BinaryTree> l)
// l is a list of single node binary trees as decribed above
{
    int n = l.Size(); // number of binary trees in l
    for (int i = 0; i < n-1; i++) { // loop n-1 times
        BinaryTree first = l.DeleteMinWeight();
        BinaryTree second = l.DeleteMinWeight();
        BinaryTree *bt = new BinaryTree(first, second);
        l.Insert(bt);
    }
}
````
O(nlog n)  
倒數第五、六行裡的 l.DeleteMinWeight()  
把最小值丟出來該怎麼做?   使用priority queue  

---
  
### Priority Queues  
In a priority queue, the element to be deleted is the one with highest (or lowest) priority.  
An element with arbitrary priority can be inserted into the queue according to its priority.  
A data structure supports the above two operations is called max (min) priority queue.  
machine service
- amount of time (min heap)
- amount of payment (max heap)  

以後看到 priority queue = heap  

**比較**  
|Representation|Insertion|Deletion|
|:---:|:---:|:---:|
|Unordered array|Θ(1)|Θ(n)|
|Unordered linked list|Θ(1)|Θ(n)|
|Sorted array|O(n)|Θ(1)|
|Sorted linked list|O(n)|Θ(1)|
|Max heap|O(log2n)|O(log2n)|  

*2是小標*  
Unordered array 和 Unordered linked list 再放入的時候都是直接放到最後沒有排序，delete最大的時候就要排序  
O(log2n)代表用tree來表示  

**Max (Min) Heap**  
Heaps are frequently used to implement priority queues. The complexity is O(log n).  
Definition: A max (min) tree is a tree in which the key value in each node is no smaller (larger) than the key values in its children (if any).  
A max heap is a complete binary tree that is also a max tree. A min heap is a complete binary tree that is also a min tree.  
雖然在heap中不一定右邊比左邊 大/小  
但是一定從 leftchild 開始填，因為必為 complete binary tree  
**Max Heap Example**  
![max-heap-examples](https://github.com/joyce-hsu/data-structure/blob/master/max-heap-examples.png)  
**Min Heap Example**  
![min-heap-examples](https://github.com/joyce-hsu/data-structure/blob/master/min-heap-examples.png)  
這裡是使用array來表示tree  
  
**Insertion Into a Max Heap**  
![insertion-heap](https://github.com/joyce-hsu/data-structure/blob/master/insertion-heap.png)  
![insertion-heap2](https://github.com/joyce-hsu/data-structure/blob/master/insertion-heap2.png)  
![insertion-heap3](https://github.com/joyce-hsu/data-structure/blob/master/insertion-heap3.png)  

````
template <class Type>
void MaxHeap<Type>::Insert(const Element <Type> &x)
// insert x into the max heap
{
    if(n == MaxSize) {HeapFull(); return;}
    n++;
    for(int i = n;1;){
        if(i == 1) 
            break;  // at root
        if(x.key <= heap[i/2].key) 
            break;  // move from parent to i
        heap[i] = heap[i/2];
        i/=2;   
    }
    heap[i] = x;
}
````  
把新來的數字放最後，再和parent比較，如果比parent大就swap，沒有就停下  
n表示目前array末的位置  
  
**Deletion From A Max Heap** 
````
template <class Type>
Element <Type>* MaxHeap <Type>::DeleteMax(Element <Type>& x)
// Delete from the max heap
{
    if (!n) {HeapEmpty(); return 0;}
    
    x = heap[1];
    Element <Type> k = heap[n];
    n--;
    for (int i = 1, j = 2; j < =n;)
        {
            if (j < n)
            {
                if (heap[j].key < heap[j+1].key)
                    j++;
            }
        // j points to the larger child
        if (k.key >= heap[j].key) break;
        heap[i] = heap[j];
        i = j; j *= 2;
        }
    heap[i] = k;
    return &x;
}
````  
![heap1](https://github.com/joyce-hsu/data-structure/blob/master/heap1.png)
![heap2](https://github.com/joyce-hsu/data-structure/blob/master/heap2.png)  

在第5個位置的10像打彈珠一樣被打上去  
以變數k暫存  
delete第五個位置的空間  
接下來和其他人比大小，找到新的位置  

delete from the max heap  
總共有兩步驟:
1. scan array **O(n)**  
2. 調整tree **O(log n)**  
相加後得到的複雜度為  **O(n)**  

**比較**  
max heap: root最大  
min heap: root最小  
insert: buttom up    
delete: top down  


**heap sort**  
如果要數字從小到大?  
step1. 建立出min heap - insert n次  **O(n\* log n)**  
step2. n個數字依序印n次 - delete n次  **O(n\* log n)**  

