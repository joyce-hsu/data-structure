**basic concepts**

1. system life cycle
2. algorithm specification
3. data abstraction
4. performance analysis & measurement

---

**system life cycle**
Requirements:設計程式要知道其input output是什麼、主要達到功能是什麼

Analysis:
1. bottom-up:從基本元件著手，再組合得到整體
2. top-down:由大局著手，為了要達使用者看到的樣子，要有什麼細節(較常用)
         
Design:
1. data objects
2. Operations:即是函式，牽涉到演算法

Refinement & coding:這時才開始寫程式，並根據output的結果不斷改良

Verification:
1. correctness proofs: selecting proved algorithms
2. testing: correctness & efficiency
3. error removal: well-document
             
---

**Evaluative judgments about programs**  

Meet the original specification?  
Work correctly?  
Document?  
Use functions to create logical units?  
Code readable?  
Use storage efficiently?  
Running time acceptable?  

---

**Data Abstraction**  
Predefined & user defined data type 
````
Struct student { 
         char last_name;
         int student_id;
         char grade; }  
````
Data type: objects & operations  
integer: +, -, *, /, %, =, ==, atoi()

---
**修飾符** 
資料欄位能不能被其他使用者使用
  
class類別-有點像struct
public公開:class裡的member(資料或成員函式)可以被所有函式存取，包含自己類別內、別的類別、甚是不屬於類別的一般函式  
private私有:只提供給相同class中的member，其他外部變數外部成員都無法使用  
protected保護:伴隨繼承概念而來，可以被相同或衍伸出來的類別使用  
  
Friend class
C ++中的好友類可以訪問將其聲明為好友的類的private和protected成員
