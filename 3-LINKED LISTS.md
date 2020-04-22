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

Template <class Type> class List {  //**這部分是被抽出的**
    friend class ListIterator <Type>;  //**所以要宣告friend class代表可以給別人用**
    public:
        List() {first = 0;};
        // List manipulation operations
        .
        .
    private:
        ListNode <Type> *first;
};
````
