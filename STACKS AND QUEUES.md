### Templates in C++

- Template function in C++ makes it easier to reuse classes and functions.  
- A template can be viewed as a variable that can be instantiated to any data type, irrespective of whether this data type is a fundamental C++ type or a user-defined type.

### Stack: a Last-In-First-Out (LIFO) list  

pop: take out an element
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

### Implementation of Stack by Array

stack是常見的data structure  
可以用array來 implement  
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
  
### Queue: a First-In-First-Out (FIFO) list

  
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
