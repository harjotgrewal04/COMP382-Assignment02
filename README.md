# **COMP382-Assignment02**
## **Group Members: Inder, Sophie, Sahil, Harjot**
## **1. Project Overview**
Find a CFG with ∑ = {a,b} and will create the language L and contains strings which will have twice as many a's as there is b's. The grammar must be proven correct and also must be justifiable why it is the simplest that could be made for this language L. 
## **2. Context-Free Grammar**
Context-Free Grammar (CFG) allows us to show languages using using variables together with production rules to convert those variables into alphabet symbols. When a string only has alphabet symbols and no variables that is when we can call it a context-free grammar. 

A CFG is defined by a 4-tuple notation:
G = (V, ∑, R, S)

V is a finite non-empty set which contains the variables <br>
∑ is the set of alphabet or symbols <br>
R is a set of rules where in the form X --> y where X must belong to V and y must be a string in V or ∑ <br>
S is a variable in the set V known as the start variable <br>

Example CFG:

E --> int          
E --> E Op E      
Op --> +          
Op --> -          
Op --> /          
Op --> *          

Generates:

E<br>
E Op E<br>
E Op E Op E<br>
int Op int Op int<br>
int + int * int <br>
int Op E<br>
E Op int <br>
int Op int<br>
int + int<br>
int * int<br>
int / int<br>
int - int<br>

Context Free Language (CFL) is the set of strings which is derivable from the orgiinal start symbol based on the given alphabet set. 

For the example earlier the language would be _L_ = { w ∈ Σ | #int(w) = #Op(w) + 1 }

## **3. Solution**
Here our G = (V, ∑, R, S) where V = {S}, ∑ = {a, b}, R: {}, and the starting symbol is S.

We can also define the context free language as:
_L_ = {w ∈ Σ | #a(w) = 2#b(w)} 

When looking at the topic, since we need twice as many a's as there are b's, we can consider the number of b's as 'n', which means the number of a's can be described as 2n.

b = n <br>
a = 2n

For a simple example, lets say we have 1 'b', then there would need to be 2 a's.

b = 1 <br>
a = 2(1) = 2

The strings we can make in this case would be "aab","aba", and "baa".

One attempt at making rules for a CFG was:

S -> aaSb <br>
S -> ϵ

This does create strings that have twice as many a's as there are b's (e.g. "aab", "aaaabb", "aaaaaabbb"), however the issue is that the strings only follow the pattern "aab". These rules do not produce any strings with the other patterns "aba" or "baa", which limits the unique strings that the CFG could produce. 

To fix this, we created two more simple CFG's representing patterns "aba" and "baa":

S -> baSa <br>
S -> ϵ

S -> abSa <br>
S -> ϵ

Now with the three CFG's we can combine them into a singular CFG:

S -> S_1 | S_2 | S_3 <br>
S_1 -> aaSb | ϵ <br>
S_2 -> abSa | ϵ <br>
S_3 -> baSa | ϵ

This CFG allows for strings to be created with more than one pattern of a's and b's, while also enforcing the requirement of having twice as many a's as there are b's.


### **3.1 Proof**


On a side note, if the number of a's and b's is an empty string (), it meets the condition of being a string in L.



### **3.2 Simplicity of Grammar**
The following reasons is what makes this grammar the simplest for the language L:

1) It only utilizes one nonterminal symbol which is S
2) The ratio of exactly 2:1 remains constant throughout every single production made
3) A easy to understand mathemtacial formula is used to prove the theory (a = 2n)
4) Removing any of the three production of strings ("aab","aba","baa") can reject the process of generating all valid strings.

For example, removing S --> aSbSaS means we do not have the aba pattern. In simpler terms, we cannot generate a string in L where the b is positioned between 2 a's. Therefore, the grammar is incomplete as it does not allow all three permutations. 

### **4. References**
- Index of /class/archive/cs/cs103/cs103.1164/lectures/18. (2016). Stanford.edu. https://web.stanford.edu/class/archive/cs/cs103/cs103.1164/lectures/18/
- Campbell, R. (2026). Sec 2.1 Context-Free Grammars Lecture slides COMP-382-ON1: Language, Computation and Machines. University of the Fraser Valley‌
- Sipser, M. (2013). Introduction to the theory of computation. Course Technology Cengage Learning.‌

