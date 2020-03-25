**basic concepts**

1. system life cycle
2. algorithm specification
3. data abstraction
4. performance analysis & measurement


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
             

**Evaluative judgments about programs**  

Meet the original specification?  
Work correctly?  
Document?  
Use functions to create logical units?  
Code readable?  
Use storage efficiently?  
Running time acceptable?  

**Data Abstraction**  
Predefined & user defined data type 
````
Struct student { char last_name;
                   int student_id;
                   char grade; }  
````
Data type: objects & operations  
integer: +, -, *, /, %, =, ==, atoi()
