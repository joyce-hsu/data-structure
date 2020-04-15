### Templates in C++

- Template function in C++ makes it easier to reuse classes and functions.  
- A template can be viewed as a variable that can be instantiated to any data type, irrespective of whether this data type is a fundamental C++ type or a user-defined type.

---

### Stack: a Last-In-First-Out (LIFO) list  

![stack](https://github.com/joyce-hsu/data-structure/blob/master/stack.png)  

pop: take out an element  
**abstract data type for stack**
````
Template <class KeyType> 
class Stack { 
// objects: A finite有限的 ordered list with zero or more elements 
public: 
Stack (int MaxStackSize = DefaultSize); 
// Create an empty stack whose maximum size is MaxStackSize 
Boolean IsFull(); 
//判斷是不是滿的
// if number of elements in the stack is equal to the maximum size 
// of the stack, return TRUE(1) else return FALSE(0) 
void Add(const KeyType& item); 
// if IsFull(), then StackFull(); else insert item into the top of the stack. 
Boolean IsEmpty(); 
//判斷是不是空的,抓東西的時候要確認
// if number of elements in the stack is 0, return TRUE(1) else return FALSE(0) 
KeyType* Delete(KeyType& ); 
// if IsEmpty(), then StackEmpty() and return 0; 
// else remove and return a pointer to the top element of the stack.
````

**Implementation of Stack by Array**

stack是常見的data structure  
可以用array來 implement(實行)  
但不是唯一的方法  
````
Private: 
int top; 
KeyType *stack; 
int MaxSize; 
template<class KeyType> Stack<KeyType>::Stack(int MaxStackSize):MaxSize(MaxStackSize)
{
stack=new KeyType[MaxSize]; 
top=-1; //判斷是不是empty
}
template<classs KeyType> 
inline Boolean Stack<KeyType>::IsFull() 
{ 
if (top==MaxSize-1) return TRUE; else return FALSE; 
} 
template<classs KeyType> 
inline Boolean Stack<KeyType>::IsEmpty() 
{ 
if (top==-1]) return TRUE; 
else return FALSE; 
}
````
::兩個冒號代表後面是member funtion  
:一個冒號代表他在初始化  


**Add to a stack**
````
Template <class KeyType> 
void Stack<KeyType>::Add(const KeyType& x) 
{
/* add an item to the global stack */ 
if (IsFull()) stack_full( ); else stack[++top]=x; 
}
````
**Delete from a stack**
````
Template <class KeyType> 
KeyType* Stack<KeyType>::Delete(KeyType& x) 
{
  /* return the top element from the stack */ 
  if (IsEmpty()) 
     { 
        stack_empty( );  /* returns and error key */ 
        return 0; 
      } 
  x=stack[top--];
  return &x; 
}
````

|stack|push|pop|
|:--:|:--:|:--:|
|queue|add|deiete|

---

### Queue: a First-In-First-Out (FIFO) list

![queue](https://github.com/joyce-hsu/data-structure/blob/master/queue.png)  

**Abstract data type of queue**
````
Template <class KeyType>
class Queue
{
// objects: A finite ordered list with zero or more elements
public:
Queue(int MaxQueueSize = DefaultSize);
// Create an empty queue whose maximum size is MaxQueueSize
Boolean IsFull();
// if number of elements in the queue is equal to the maximum size of
// the queue, return TRUE(1); otherwise, return FALSE(0)
void Add(const KeyType& item);
// if IsFull(), then QueueFull(); else insert item at rear of the queue
Boolean IsEmpty();
// if number of elements in the queue is equal to 0, return TRUE(1)
// else return FALSE(0)
KeyType* Delete(KeyType&);
// if IsEmpty(), then QueueEmpty() and return 0;
// else remove the item at the front of the queue and return a pointer to it
};
  ````
**Implementation 1: using array**  
````
Private: 
int front,rear;  
KeyType *queue;  
int MaxSize;  
Template<class KeyType>  
Queue<KeyType>::Queue(int MaxQueueSize):MaxSize(MaxQueueSize) { 
queue=new KeyType[MaxSize];  
front=rear=-1;  
}  

template<classs KeyType>  
inline Boolean Queue<KeyType>::IsFull() {  
if (rear==MaxSize-1) 
    return TRUE;  
else 
    return FALSE;  
}  

template<classs KeyType>  
inline Boolean Stack<KeyType>::IsEmpty() {  
if (front==rear) 
    return TRUE;  
else 
    return FALSE;  
}
````

**Add to a queue**
````
Template <class KeyType>  
void Queue<KeyType>::Add(const KeyType& x) {
/* add an item to the global stack */ 
if (IsFull()) 
    QueueFull( ); //判斷是否為滿
else 
    queue[++rear]=x;  
 }
````

**Delete from a queue**
````
Template <class KeyType>  
KeyType* Queue<KeyType>::Delete() {
/* return the top element from the stack */ 
if (IsEmpty()) { 
    QueueEmpty( ); /* returns and error key */ 
    return 0; 
} 
x=queue[++front]; //front++之後記錄資料
return x;  
}
````

假設一個Queue已滿，若刪掉第一個位置，因為最後一個位置仍有值  
這時候QueueFull()會判斷為full  
所以移除持要空間搬移data movement  
或考慮QueueFull()的判斷法  
又或者寫其他的判斷法補足  

**Implementation 2: regard an array as a circular queue**
![circular queue1](https://github.com/joyce-hsu/data-structure/blob/master/circular-queue-1.png)  

可以填滿嗎?
為什麼不能填滿呢?  
填滿之後front = 0 rear = 0  
就無法分辨 Queue 滿的 或 空的

![circular queue2](https://github.com/joyce-hsu/data-structure/blob/master/circular-queue-2.png)  

左圖變成右圖:先刪掉 J1~J4,再加入 J6~J9  

**Add to a circular queue**  
````
Template<class KeyType> 
void Queue<KeyType>::Add(const KeyType& x) { 
int newrear=(rear+1)%MaxSize; //MaxSize = 總共的格數 
if (front==newrear) 
    QueueFull(); 
else 
    queue[rear=newrear]=x;  //可分為兩個指令rear=newrear，queue[rear]=x;
}
````

**Delete from a circular queue**
````
Template<class KeyType> 
KeyType* Queue<KeyType>::Delete(KeyType& x) {  
/* remove front element from the queue */  
if (front == rear) {  
    QueueEmpty(); //先判斷是否為空，空的話就跳過
    return 0; 
} 
front = (front+1) % MaxSize; 
x=queue[front]; 
return &x; 
}
````

---

### A Mazing Problem  

![迷宮](https://github.com/joyce-hsu/data-structure/blob/master/maze.png)  

**a possible representation**  

![方位](https://github.com/joyce-hsu/data-structure/blob/master/dir.png)  

**a possible implementation**   
````
typedef struct { 
    int vert; 
    int horiz; 
} offsets; 

offsets move[8]; /*array of moves for each direction*/

next_row = row + move[dir].vert; 
next_col = col + move[dir].horiz;
````
![方位表](https://github.com/joyce-hsu/data-structure/blob/master/dir-table.png)  

**Use stack to keep pass history**  
因為可能有走進死胡同要回頭找路的情況  
故需要Last-In-First-Out的stack幫忙記路  
````
typedef struct {  
    int row; 
    int col; 
    int dir; 
} item;  
item stack[m*p];  //一個迷宮共m*p格
````
Program 3.15
````
initialize stack to the maze entrance coordinates and direction east ;
while (stack is not empty){
    (i, j, dir) = coordinates and direction deleted from top of stack ;
    while (there are more moves){
        (g, h) = coordinates of next move ;
        if ((g == m) && (h == p)) 
            success ;
            
         if ((!maze[g][h]) // legal move  
               && (!mark[g][h]) // haven’t been here before {
             mark[g][h] = 1 ;
             dir = next direction to try ;
             add (i, j, dir) to top of stack ;
             i = g ; j = h ; dir = north ;
         }
     }
}
cout << “not path found” << endl ;
````

Program 3.16
````
void path (int m, int p)
/*Output a path (if any) in the maze;
maze[0][i] = maze[m+1][i] = maze[j][0] = maze[j][p+1] = 1, 0<= i <= p+1, 0<= j <= m+1.*/
// 在迷宮外圍一圈1，這樣就不用判斷邊界，因為遇到1會直接判斷為死路
{
//start at (1,1)
mark[1][1] = 1 ;
Stack<items> stack(m*p) ;
items temp ;
temp.x = 1 ; temp.y = 1 ; temp.dir = E ;
stack.Add(temp) ;

while(!stack.IsEmpty()) // stack not empty
{
    temp = *stack.Delete(temp) ; // unstack
    int i = temp.x ; int j = temp.y ; int d = temp.dir ;
    while(d < 8) // move forward 
        {
        int g = i + move[d].a ; int h = j + move[d].b ;
        if ((g == m) && (h == p)) { // reached exit
            //output path
            cout << stack 
            cout << i << “ “ << j << endl ; // last two squares on the path
            cout << m << “ “ << p << endl ;
            return ;
            }
        if ((!maze[g][h]) && (!mark[g][h])) { // new position
            mark[g][h] = 1 ;
            temp.x = i ; temp.y = j ; temp.dir = d+1 ;
            stack.Add(temp) ; // stack it
            i = g ; j = h ; d = N ; // move to (g, h)
            }
        else 
            d++ ; // try next direction
        }
}
cout << “no path in maze “ << endl ;
}
````

---

### Evaluation of Expressions  

How to generate the machine instructions corresponding to a given expression?
如何生成出所給表達式相對應的機器指令？  
precedence rule + associative rule  
要遵守括號優先和四則運算先乘除後加減  

|user|compiler|
|:---:|:---:|
|**Infix**|**Postfix**|
|2 + 3 * 4|234*+ |
|a * b + 5|ab * 5+ |
|(1 + 2) * 7 |12+7 * |
|a * b / c |ab * c/ |
|(a / (b - c + d)) * (e-a) * c|abc-d+/ea-* c * |
|a / b - c + d * e - a * c|ab/c-de* ac*-+ |

Postfix: no parentheses, no precedence  

![例一]()  

**Goal: infix --> postfix**  
Assumptions:  
operators: +, -, * , /, %  
operands:  single digit integer  

*方法一*  
(1) Fully parenthesize expression  全部的括號都標示出來
a / b - c + d * e - a * c -->  ((((a / b) - c) + (d * e)) - a * c))  

(2) All operators replace their corresponding right parentheses.  
所有的運算子找到對應的右括號  
![如圖]()  
(3) Delete all parentheses.  將右括號以運算符號取代並去掉左括號
    ab/c-de*+ac*-  
    
 > 但此方法有兩個步驟 
    
*方法二*  
訂出運算符號的優先順序  
|Priority|Operator|
|:---:|:---:|
|1|Unary minus(例如負號), !|
|2|* , / , % |
|3|+ , -|
|4|< , <= , >= ,>|
|5|== , != |
|6| && |
|7| || |

![例二]()  


