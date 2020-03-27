###Arrays
Array: a set of index and value

`data structure`  
For each index, there is a value associated with that index.  


`representation (possible)`  
implemented by using consecutive memory.  
Example: int list[5]: list[0], …, list[4] each contains an integer  

|      | 0 | 1 | 2 | 3 | 4 |
|------|---|:--|---|---|--:|
| List |   |   |   |   |   |

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

###Adding a new Term
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
