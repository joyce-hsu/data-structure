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
