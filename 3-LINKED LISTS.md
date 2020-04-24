### linked list 鏈結序列  
牽扯到比較多的pointer(指標)  
推薦以圖表示比較好懂  

**Introduction**  
array:  
是連續的記憶體空間  
因為陣列資料數先宣告，當資料量變動大時，容易浪費空間  
資料刪減時常要資料搬移  
  
linked lists可以解決以上問題  
但缺點是linked lists的pointer要控制好  
否則亂指或丟失pointer時資料也容易遺失  
  
double linked list 可以多一層保障  
(雙向鏈接串列)  

**Composite Classes**  Program 4.1 
````
class ThreeLetterList; // forward delcarion 宣告
class ThreeLetterNode {
    friend class ThreeLetterList;
    private:
        char data[3];
        ThreeLetterNode * link;
};
class ThreeLetterList {
    public:
        // List Manipulation operations
        .
        .
    private:
        ThreeLetterNode *first;
};
````

**Nested Classes**  
  
The Three Letter List problem can also use nested classes to represent its structure.
````
class ThreeLetterList {
    public:
        // List Manipulation operations
        .
        .
    private:
        class ThreeLetterNode { // nested class
        public:
            char data[3];
            ThreeLetterNode *link;
        };
    ThreeLetterNode *first;
};
````
Nested Classes-class裡有class  
優點:可以存取外部類別的private成員  
缺點:內部的class其他的class不能共用  
  
**Pointer Manipulation in C++**   
Two pointer variables of the same type can be compared.  
  x == y, x != y, x == 0   
   
![asssignment](https://github.com/joyce-hsu/data-structure/blob/master/asssignment.png)  
注意: \*x = \*y代表指到的內容會asssignment一樣   

**create a linked list with two nodes**   
  
![twonodes](https://github.com/joyce-hsu/data-structure/blob/master/twonodes.png)  
````
void List::Create2( ) {
    /* create a linked list with two nodes */ 
    first = new ListNode(10); 
    first->link = new ListNode(20); 
}
ListNode::ListNode(int element=0) { 
    data = element; 
    link = NULL;
}
````
**List Insertion : Insert a node after a specific node**  
  
![list-insertion](https://github.com/joyce-hsu/data-structure/blob/master/list-insertion.png)  
````
void List::Insert50 (ListNode *x) {
    /* insert a new node with data = 50 into the list */ 
    ListNode *t=new ListNode(50); 
    if (!first) { //!first = true 代表linked lists是空的
        first = t; 
        return; 
    } //insert after x 
t->link=x->link; 
x->link=t; 
}
````
pointer指定的順序不可以相反   
否則會有資料遺失  

**List Deletion**   
  
![list-deletion](https://github.com/joyce-hsu/data-structure/blob/master/list-deletion.png)  
想要delete的node可以存進另一個linked lists  
未來需要node時直接從裡面拿  
省去和memory要空間的動作

---

**List Iterator**  
- A list iterator is an object that is used to traverse all the elements of a container class.
- ListIterator\<Type> is delcared as a friend of both List\<Type> and ListNode\<Type>.
- A ListIterator\<Type> object is initialized with the name of a List<Type> object l with which it will be associated.
- The ListIterator\<Type> object contains a private data member current of type ListNode\<Type> *. At all times, current points to a node of list *l*.
- The ListIterator\<Type> object defines public member functions NotNull(), NextNotNull(), First(), and Next() to perform various tests on and to retrieve elements of *l*.
- 老師說:把list中比較general的operation拿出來寫成class給全部的linked list用，例如:scan, number of node, not NULL(), NextNotNull(), First()  
  
**Program 4.8 Template of Linked Lists**  
````
Enum Boolean { FALSE, TRUE};
template <class Type> class List;
template <class Type> class ListIterator;

template <class Type> class ListNode {
    friend class List<Type>;
    friend class ListIterator <Type>;
    private:
        Type data;
        ListNode *link;
};

Template <class Type> class List {  
    friend class ListIterator <Type>;  //**要宣告friend class代表可以給別人用**
    public:
        List() {first = 0;};
        // List manipulation operations
        .
        .
    private:
        ListNode <Type> *first;
};
template <class Type> class ListIterator {  //**這部分是被抽出的**
    public:
        ListIterator(const List<Type> &l): list(l), current(l.first) {};
        Boolean NotNull();
        Boolean NextNotNull();
        Type * First();
        Type * Next();
    Private:
        const List<Type>& list; // refers to an existing list
        ListNode<Type>* current; // points to a node in list
};
````

---

**Program 4.11 Attaching A Node To The End Of A List**  
````
Template <class Type>
Void List<Type>::Attach(Type k)
{
ListNode<Type>*newnode = new ListNode<Type>(k);
if (first == 0) first = last =newnode;
else {
    last->link = newnode;
    last = newnode;
    }
};
````  

**Program 4.12 Inverting a list**  
````
Template <class Type>
Void List<Type>:: Invert()
// A chain x is inverted so that if x=(a1,…an)
//then, after execution, x=(an,…,a1)
{
ListNode<Type>*p = first,*q=0; //q trails p
while (p)
    {
    ListNode<Type> *r=q; //r trails q
    q=p;
    p=p->link;
    q->link=r;
    }
    first=q;
};
````
將list轉置(反轉)  
![inverting a list](https://github.com/joyce-hsu/data-structure/blob/master/inverting-a-list.png)  


**Program 4.13 Concatenating Two Chains**  
````
Template <class Type>
void List<Type>:: Concatenate(List<Type> b)
// this = (a1, …, am) and b = (b1, …, bn) m, n ≥ ,
// produces the new chain z = (a1, …, am, b1, bn) in this.
{
    if (!first) { first = b.first; return;}
    if (b.first) {
         for (ListNode<Type> *p = first; p->link; p = p->link); // no body
         p->link = b.first;
     }
}
````
for (ListNode<Type> *p = first; p->link; p = p->link);  
  這句很特別，for loop裡沒有特別要做什麼事，只是把p移到linked list最末  

**List Destructor**
````
Template <class Type>
List<Type>::~List()
// Free all nodes in the chain
{
    ListNode<Type>* next;
    for (; first; first = next) {
        next = first->link;
        delete first;
    }
}
````
**Diagram of A Circular List**  
![A Circular List](https://github.com/joyce-hsu/data-structure/blob/master/circular-list.png)  

**Linked Stacks and Queues**  
![linked stacks and queues](https://github.com/joyce-hsu/data-structure/blob/master/linked-stacks-and-queues.png)  
Stacks and Queues不只可以用array implement  
linked list也可以  

---

### Revisit Polynomials  
優點:解決sparse的問題  
缺點:(老師說自己想,但我目前想不到嗚嗚)  

**Program 4.20 Polynomial Class Definition**  
````
struct Term
// all members of Terms are public by default
{
    int coef; // coefficient
    int exp; // exponent
    void Init(int c, int e) {coef = c; exp = e;};
};

class Polynomial
{
    friend Polynomial operator+(const Polynomial&, const Polynomial&);
    private:
    List<Term> poly;
};
````  
operator+  : 把operator "+" overload成想要的多項式的 +  

**Operating On Polynomials**  
![polynomial-linked-1](https://github.com/joyce-hsu/data-structure/blob/master/polynomial-linked-1.png)
![polynomial-linked-2](https://github.com/joyce-hsu/data-structure/blob/master/polynomial-linked-2.png)  
相加:比array容易~!!  

**Represent polynomial as circular list**  
![polynomial-circular-list](https://github.com/joyce-hsu/data-structure/blob/master/polynomial-circular-list.png)  
因為是circular list 所以要加一個 head node

---

### Free Pool    
node的資收場
不浪費太多的overhead去creat新的node  
(overhead:好像翻做後勤資源)  
````
template < class Type>
ListNode <Type>* CircList::GetNode()
// Provide a node for use
{
ListNode <Type> *x;
if( !av ) 
    x = new ListNode<Type>;
else{ 
    x = av; 
    av = av -> link;
    }
return x;
}
````
av : available linked list 表示free pool裡有東西  
!av表示free pool is empty  

**把node丟進free pool**  
口語上可以說return a node
````
template <class Type>
void CircList<Type>::RetNode( ListNode<Type> *x
//Free the node pointed to by x
{
    x -> link = av;
    av = x;
}
````
**Erase the circular list pointed to by first**  
````
template <class KeyType>
void CircList<Type>::~CirList()
//Erase the circular list pointed to by first
{
    if( first )
    {
        ListNode* second = first -> link; //(1)
        first->link = av; //(2)
        av =second; //(3)
        first =0; //(4)
        }
}
````
![erase-circular-list](https://github.com/joyce-hsu/data-structure/blob/master/erase-circular-list.png)  

---

### Equivalence Relations  
A relation over a set, S, is said to be an equivalence relation over S.  
iff : it is symmertric, reflexive, and transitive over S.
reflexive, x=x  
symmetric, if x=y, then y=x  
transitive, if x=y and y=z, then x=z 

iff:⇔ P iff Q( P if and only if Q)

**Examples**  
- Input: pairs of numbers
0≡4, 3≡1, 6≡10, 8≡9, 7≡4, 6≡8, 3≡5, 2≡11, 11≡0
- Output: equivalent sets
three equivalent classes {0,2,4,7,11}; {1,3,5}; {6,8,9,10}  

**A Rough Algorithm to Find Equivalence Classes** 
````
void equivalenec()
{
    initialize;
    //Phase 1
    while (there are more pairs) {
        read the next pair <i,j>;
        process this pair;
    }
    initialize the output;
    //Phase 2
    do {
        output a new equivalence class;
        } while (not done);
}
````
太rough了!
What kinds of data structures are adopted?
只能表示需要兩個步驟
phase1:讀數字;phase2依關係分類  

![Lists After Pairs input](https://github.com/joyce-hsu/data-structure/blob/master/lists-after-pairs-input.png)

Program 4.28:
````
void equivalence()
{
    read n; // read in number of objects
    initialize seq to 0 and out to FASLE;
    while more pairs // input pairs
    {
        read the next pair (i,j);
        put j on seq[i] list;
        put i on seq[j] list;
    }
    for( i = 0; i < n; i++ )
        if( out[i] == FALSE){
            out[i] = TRUE;  //紀錄是否ouput過
            output the equivalence class that contains object i
            //direct equivalence
            //Compute indirect equivalence using transitivity
        }
}// end of equivalence
````

program 4.29:  
````
enum Boolean { FALSE, TRUE };
class ListNode{
    friend void equivalence();
    private:
        int data;
        ListNode *link;
        ListNode(int);
};
typedef ListNode *ListNodePrt;

ListNode::ListNode(int d){
    data = d;
    link = 0;
}

void equivalence()
// Input the equivalence pairs an output the equivalence classes
{
    ifstream inFile(“equiv.in”, ios::in); //”equiv.in” is the input file
    if(!inFile){
        cerr << “Cannot open input file ”<< endl;
        return;
    }
    int i, j, n;
    inFile >> n; // read number of objects
    // initialize seq and out
    ListNodePtr *seq = new ListNodePtr[n];
    Boolean *out = new Boolean[n];
    for( i = 0; i < n ; i++){
        seq[i] = 0;
        out[i] = FALSE;
    }
    
    // Phase 1: input equivalence pairs
    inFile >> i >> j ;
    while( inFile.good()){ // check end of file
        ListNode *x = new ListNode(j); x->link = seq[i];
        seq[i] = x // add j to seq[i] ex.add 4 to seq[0]
        ListNode *y = new ListNode(i); y->link = seq[j];
        seq[j] = y // add i to seq[j]
        inFile >> i >> j;
    }
    
    // Phase 2: output equivalence classes
    for( i = 0; i < n; i++)
        if( out[i] == FALSE){ // needs to be output
            cout << endl << “A new class: “ << i; // for example, i=0. Output: 0
            out[i] = TRUE;
            ListNode *x = seq[i]; ListNode *top = 0; //init stack
            
            while(1){ // find rest of class
                while(x){ // process the list
                    j = x->data; // when i=0. j=11
                    if( out[j] == FALSE ){
                        cout << “,” << j; //when i=0 in first round, output:11
                        out[j] = TRUE;
                        //*push*
                        ListNode *y = x -> link; //when i=0 in the first round, y=4
                        x -> link = top;
                        top = x; // in stack, top points to node 11
                        x = y;
                    }
                    else x = x->link;
                }// end of while(x)
                //*pop*
                if( !top ) break;
                else{
                    x = seq[top->data];
                    top = top->link; // unstack
                }
            } // end of while(1)
            
        } // end of if( out[i] == FALSE)
        
        //delete
        for( i = 0; i < n; i++ )
            while( seq[i]){
                ListNode *delnode = seq[i];
                seq[i] = delnode->link;
                delete delnode;
            }
        }
    delete [] seq; delete [] out;
} // end of equivalence
````
從seq\[0]開始逐一探索、印出(11、4)並存入stack，11 先加進stack，然後才是 4    
因為stack是FILO，所以seq\[0]都印出後，探索seq\[4]  
探索seq\[4]時，將 7 印出並加入stack，隨後開始探索seq\[7]  
由於seq\[7]中的 4 已經被印出，所以stack pop out 11  
接著開始探索seq\[11]，0 被印過了就略過，發現 2 沒有印過，所以將 2 印出並push in stack  
隨後從stack pop out 2，探索seq\[2]，但seq\[2]中的 11 已印出，stack裡面也空了(!top)，故結束整個while(1)  

統整一下  
phase2的for迴圈( i = 0; i < n; i++ )，每次迴圈時會做一件大事: **確認seq\[i]是否印出**  

若seq\[i]沒有印出過，則進入while(1)迴圈，該迴圈主要有兩件事：
1. 將seq\[i]連接的linked list數字都印出  while(x)  
x 會不斷往下指到seq\[i]連接的linked list，當x不存在代表該列已印完
  - x 不存在，進入事件2.  
  - x 存在，將x指到的數字印出，並加入stack  
2. 確認stack裡還有沒有數值，top是否存在  
  - top不存在，跳出while(1)，進入下次的for迴圈  
  - top存在，將 x 指到seq\[top->data]進行while(x)  
  
[參考影片](https://www.youtube.com/watch?v=EevziMd4MMs)
  
---

### Sparse Martix  
new scheme  
Each column (row): a circular linked list with a head node  
![linked representation sparse matrix](https://github.com/joyce-hsu/data-structure/blob/master/linked-representation-sparse-matrix.png) 
為表示方便才這樣畫，除了黑框白底的node，其實只有一藍三黃的node  
For an n\*m sparse matrix with r nonzero terms,  
the number of nodes needed is max{n, m} + r + 1.  
![headnode-entrynode](https://github.com/joyce-hsu/data-structure/blob/master/headnode-entrynode.png)   
黃色三欄位、黑色五欄位  
down連同一行的元素；right連同一列的元素  
program 4.30:  
````
enum Boolean { FALSE, TRUE };
struct Triple { int value, row, col ; };
class Matrix ; //forward declaration
class MatrixNode {
    friend class Matrix ;
    //for reading in a matrix
    friend istream& operator>>(istream&, Matrix&) ;
    private:
        MatrixNode *down, *right ;
        Boolean head ;
        union { //anonymous union
            MatrixNode *next ;
            Triple triple ;
        };
        MatrixNode(Boolean, Triple *) ; //constructor
    };
MatrixNode::MatrixNode(Boolean b, Triple *t) //constructor
{
    head = b ;
    if (b) { right = next = down = this;} //row/column head node
    else triple = *t ; //head node for list of headnodes OR element
    //node
}
typedef MatrixNode * MatrixNodePtr ;
//to allow subsequent creation of array of pointers
class Matrix{
    friend istream& operator>>(istream&, Matrix&) ;
    public:
        ~Matrix() ; //destructor
    private:
        MatrixNode *headnode ;
};
````
Boolean head:因為想用同一個MatrixNode表示head和matrix的數值，所以需要boolean來判斷是否為head  
union:二選一，如果是head選MatrixNode \*next，如果不是head選Triple triple(value,row,col)  
用linked list方式表達matrix的話，做transpose很簡單，只要raw跟col對調即可  

---

### Doubly Linked List  
Move in forward and backward direction.  
  
Node in doubly linked list  
left link field (llink)  
data field (item)  
right link field (rlink)  
  
program 4.33:
````
class DblList ;
class DblListNode {
    friend class DblList ;
    private:
        int data ;
        DblListNode *llink, *rlink ;
};
class DblList {
    public:
        //List manipulation operations
    private:
        DblListNode *first ; //points to head node
};
````
  
![doubly-linked-list-headnode](https://github.com/joyce-hsu/data-structure/blob/master/doubly-linked-list-headnode.png)    
A head node is also used in a doubly linked list to allow us to implement our operations more easily.  
圖比較難看懂，head node的rlink指first node；llink指final node
empty的話指向自己  

**Insertion into an empty doubly linked circular list**  
![insertion-empty-doublylinkedcircularlist](https://github.com/joyce-hsu/data-structure/blob/master/insertion-empty-doublylinkedcircularlist.png)  

**Insert**  
````
void DblList::Insert(DblListNode *p, DblListNode *x)
//insert node p to the right of node x
{
    p->llink = x ; //(1)
    p->rlink = x->rlink ; //(2)
    x->rlink->llink = p ; //(3)
    x->rlink = p ; //(4)
}
````  
![insert-doublylinkedcircularlist](https://github.com/joyce-hsu/data-structure/blob/master/insert-doublylinkedcircularlist.png)  

**Delete**  
````
void DblList::Delete(DblListNode *x) {
    if(x == first) cerr<<“Deletion of head node not permitted”<<endl ;
else {
    x->llink->rlink = x->rlink ; //(1)
    x->rlink->llink = x->llink ;//(2)
    delete x ;
    }
}
````
![delete-doublylinkedcircularlist](https://github.com/joyce-hsu/data-structure/blob/master/delete-doublylinkedcircularlist.png)  

**老師閒聊**  
data base  
file是什麼構成的?存在disk磁碟機裡就是由disk構成  
disk最小儲存單位是block  
檔案的data structrue 就是doubly linked list  
block之間雙向pointer串連  
single linked list也可以，只是風險較高，丟失一個pointer就找不回資料了
