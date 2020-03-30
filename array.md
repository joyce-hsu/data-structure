### Arrays
Array: a set of index and value

`data structure`  
For each index, there is a value associated with that index.  


`representation (possible)`  
implemented by using consecutive memory.  
Example: int list[5]: list[0], …, list[4] each contains an integer  

|      | 0 | 1 | 2 | 3 | 4 |
|------|---|:--|---|---|--:|
| List |   |   |   |   |   |

---

**用array表示多項式**  

Polynomial Representation 1
private:
````
int degree;  // degree ≤ MaxDegree
float coef [MaxDegree + 1];
````
     x^4+10x^3+3x62+1
|          | 0 | 1 | 2 | 3  | 4 |
|----------|---|:--|---|----|--:|
|CoeffArray| 1 | 0 | 3 | 10 | 1 |

指數在index:缺點次方差很多的話會浪費空間(ex. 2x^1000+1)  

Polynomial Representation 3  
|          | a start | a finish | b start |    | b finish |
|----------|---------|:---------|---------|----|---------:|
|CoeffArray| 1 | 0 | 3 | 10 | 1 |



storage requirements:  
start, finish, 2*(finish-start+1)  
nonsparse: twice as much as (1) when all the items are nonzero  
````
class term { 
friend Polynomial; 
private: 
float coef; // coefficient 
int exp; // exponent 
}; 
class Polynomial; // forward delcaration { 
private:
static term termArray[MaxTerms];   //static 不同的多項式會使用相同的空間
static int free; //告訴我們那些index是沒有用到的，好處在於新的多項式可以從free開始存
int Start, Finish; 
} 
term Polynomial:: termArray[MaxTerms]; 
int Polynomial::free = 0; // location of next free location in temArray
````

**Adding a new Term**
````
void Polynomial::NewTerm(float c, int e)
// Add a new term to C(x)
{
if (free >= MaxTerms) {
cerr << “Too many terms in polynomials”<< endl;
exit();
}


termArray[free].coef = c;  //係數
termArray[free].exp = e;  //次方
free++;
} // end of NewTerm
````
---

**兩個多項式相加**
````
Polynomial Polynomial:: Add(Polynomial B)
// return the sum of A(x) ( in *this) and B(x)
{
Polynomial C; int a = Start; int b = B.Start; C.Start = free; float c;
while ((a <= Finish) && (b <= B.Finish))
switch (compare(termArray[a].exp, termArray[b].exp)) {
case ‘=‘:
c = termArray[a].coef +termArray[b].coef;
if ( c ) NewTerm(c, termArray[a].exp);
a++; b++;
break;
case ‘<‘:
NewTerm(termArray[b].coef, termArray[b].exp);
b++;
case ‘>’:
NewTerm(termArray[a].coef, termArray[a].exp);
a++;
} // end of switch and while
// add in remaining terms of A(x)
for (; a<= Finish; a++)
NewTerm(termArray[a].coef, termArray[a].exp);
// add in remaining terms of B(x)
for (; b<= B.Finish; b++)
NewTerm(termArray[b].coef, termArray[b].exp);
C.Finish = free – 1;
return C;
} // end of Add
````
Analysis: O(n+m) where n (m) is the number of nonzeros in A(B).  
複雜度分析 因為每個項都要比較，所以complexity是n+m

---

**Disadvantages of Representing Polynomials by Arrays**  
What should we do when free is going to exceed MaxTerms?  
- Either quit or reused the space of unused polynomials. But costly.  
回收使用:寫一個destractor(解構函式)  告訴電腦這個多項式已經用過了  
有什麼缺點? 可能有些地方已用過，但有些空間仍占用，所以當初填新的方程式的函數就不能從free來寫  
需要重整:把有占用的移到一起(作業系統的memory management；磁碟管理 磁碟重整的概念)  
If use a single array of terms for each polynomial, it may alleviate the above issue but it penalizes the performance of the program due to the need of knowing the size of a polynomial beforehand  

---

**Sparse Martrix**  
一般怎麼表示陣列:宣告一個二維矩陣  
如果在矩陣中，多數的元素並沒有資料，稱此矩陣為sparse matrix   
只要記錄非0位置的值 Use triple <row, column, value>  

**Transpose a Matrix**  
1. for each row i take element <i, j, value> and store it  
in element <j, i, value> of the transpose.  
difficulty: where to put <j, i, value>  
(0, 0, 15) ====> (0, 0, 15)  
(0, 3, 22) ====> (3, 0, 22)  
(0, 5, -15) ====> (5, 0, -15)  
(1, 1, 11) ====> (1, 1, 11)  
Move elements down very often.  
右手邊並沒有一row的大小排列所以要重新排序

2. For all elements in column j, place element <i, j, value> in element <j, i, value>

````
SparseMatrix SparseMatrix::Transpose()  
// return the transpose of a (*this)  
{  
SparseMatrix b;  
b.Rows = Cols; // rows in b = columns in a  
b.Cols = Rows; // columns in b = rows in a  
b.Terms = Terms; // terms in b = terms(項數) in a  
if (Terms > 0) // nonzero matrix 
{  
int CurrentB = 0;  
for (int c = 0; c < Cols; c++) // transpose by columns  
for (int i = 0; i < Terms; i++) // find elements in column c  
//逐項檢查,但只找column為c的交換row跟col
if (smArray[i].col == c) {  
b.smArray[CurrentB].row = c;  
b.smArray[CurrentB].col = smArray[i].row;  
b.smArray[CurrentB].value = smArray[i].value;  
CurrentB++;  //現在b.array的所指到的位置
}  
} // end of if (Terms > 0)  
return b;  
} // end of transpose
````
Time Complexity O(terms * cols)
兩個for迴圈，外圈跑cols，內圈跑terms  

這個演算法的缺點:效率較差，每次col迴圈，每個term要逐項檢查  
如果不是Sparse Martrix複雜度就會變成O(columns * columns * rows)  
(terms = columns * rows)

---

`Solution`  
Determine the number of elements in each column of the original matrix.  
Determine the starting positions of each row in the transpose matrix.  

![alt 文字](https://github.com/joyce-hsu/data-structure/blob/master/SparseMatrixTranspose.png)

index 表示原本的col
rowsize 是原本數字為index之col有幾個
start 表示新的陣列的開始位置(用前幾項rowsize的和或rowsize+rowstart)

**Fast Matrix Transposing**   
````
SparseMatrix SparseMatrix::Transpose()
// The transpose of a(*this) is placed in b and is found in Q(terms + columns) time.
{
int *Rows = new int[Cols];
int *RowStart = new int[Cols];
SparseMatrix b;
b.Rows = Cols; b.Cols = Rows; b.Terms = Terms;
int i;
if (Terms > 0) // nonzero matrix
{
// compute RowSize[i] = number of terms in row i of b
for ( i = 0; i < Cols; i++) RowSize[i] = 0; // Initialize；複雜度:O(columns)

for ( i = 0; i < Terms; i++) RowSize[smArray[i].col]++;
// RowStart[i] = starting position of row i in b
// 此迴圈在做RowStart[]的計數；複雜度:O(terms)
// smArray[0].col = 0 -> RowSize[0]++
// smArray[1].col = 4 -> RowSize[4]++
// smArray[2].col = 1 -> RowSize[1]++
// smArray[3].col = 1 -> RowSize[1]++ (此時RowSize[1] = 2)



RowStart[0] = 0;
for (i = 1; i < Cols; i++) RowStart[i] = RowStart[i-1] + RowSize[i-1];
// 算出RowStart；複雜度:O(columns-1)

//開始transpore；複雜度:O(terms)
for (i =0; i < Terms; i++) // move from a to b
{
int j = RowStart[smArray[i].col];
// 對每個term檢查col
b.smArray[j].row = smArray[i].col;
b.smArray[j].col = smArray[i].row;
b.smArray[j].value = smArray[i].value;
RowStart[smArray[i].col]++;  //進行一次迴圈後原本col為0的起始位置從0移到1
} // end of for
} // end of if
delete [] RowSize;
delete [] RowStart;
return b;
} // end of FastTranspose
````

如果不是Sparse Martrix複雜度就會變成O(columns * rows)  
(terms = columns * rows)

---

**Two Dimensional Array Row Major Order**  
一行存完再存一行(橫)  
Column Major就是一列存完再存一列(直)  
會影響到每個element的記憶體位置

**String**  
- Usually string is represented as a character array.  
老師問:如何存中文,如何做中文處理,可以修資料檢索
- General string operations include comparison, string concatenation, copy, insertion, string matching, printing, etc.

**String Matching: Straightforward solution**  
![alt 文字](https://github.com/joyce-hsu/data-structure/blob/master/StringMatching.png)  
一一比對不像的話shift(平移)一格  
要達成平移的話要有個變數,去改變比對的t字串的起始位置  
Worst-case complexity is in θ(mn)  
