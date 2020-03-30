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
複雜度分析 因為每個像都要比較，所以complexity是n+m

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


