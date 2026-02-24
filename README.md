# **COMP 382 - Assignment 2**

## **Group Members: Inder, Sophie, Sahil, Harjot**

## **1. Project Overview**
Let ∑ = {a,b}. Find a CFG generating the language L of strings which have twice as many a's as there are b's. The grammar must be proven correct and justified in why it is one of the simplest that could be made for this language L.

## **2. Context-Free Grammar**
A Context-Free Grammar (CFG) is a set of rules that defines the structure of a language. It allows us to show languages using variables together with production rules to convert those variables into alphabet symbols. When a string only has alphabet symbols and no variables that is when we can call it a context-free grammar. 

A CFG is defined by a 4-tuple notation:

G = (V, ∑, R, S)

- V is a finite non-empty set that contains the variables
- ∑ is a set of alphabet or symbols
- R is a set of rules in the form X &#8594; y, where X must belong to V and y must be a string in V or ∑
- S is a variable in the set V, also known as the start variable

Example CFG:

E &#8594; int          
E &#8594; E Op E      
Op &#8594; +          
Op &#8594; -          
Op &#8594; /          
Op &#8594; *          

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

For the earlier example, the language would be _L_ = { w ∈ Σ | #int(w) = #Op(w) + 1 }

## **3. Solution**
Let G = (V, ∑, R, S) be our grammar, where V = {S}, ∑ = {a, b}, R: {}, and the starting symbol be S.

We can also define the context free language as:

_L_ = {w ∈ Σ | #a(w) = 2#b(w)} 

When looking at the topic, since we need twice as many a's as there are b's, we can consider the number of b's as 'n', which means the number of a's can be described as 2n.

b = n <br>
a = 2n

For a simple example, let's say we have 1 'b'. Then there would need to be 2 a's.

b = 1 <br>
a = 2(1) = 2

The strings we can make in this case would be "aab", "aba", and "baa".

One attempt at making rules for a CFG was:

S &#8594; aaSb <br>
S &#8594; ϵ

While this does create strings that have twice as many a's as there are b's (e.g. "aab", "aaaabb", "aaaaaabbb"), the issue is that the strings only follow the pattern "aab". These rules do not produce any strings with the other patterns "aba" or "baa", which limits the unique strings that the CFG could produce. 

To fix this, we created two more simple CFG's representing patterns "aba" and "baa":

S &#8594; baSa <br>
S &#8594; ϵ

S &#8594; abSa <br>
S &#8594; ϵ

We can now combine the three CFG's into a singular CFG:

S &#8594; S<sub>1</sub> | S<sub>2</sub> | S<sub>3</sub> <br>
S<sub>1</sub> &#8594; aaSb | ϵ <br>
S<sub>2</sub> &#8594; abSa | ϵ <br>
S<sub>3</sub> &#8594; baSa | ϵ 

This CFG allows for strings to be created with more than one pattern of a's and b's, while also enforcing the requirement of having twice as many a's as there are b's.

### **3.1 Proof**
1.) Soundness of this grammar ensures that all strings produced are valid.<br>

Base Case: S &#8594; ϵ, meaning that there are 0 a's and 0 b's. Therefore, 0(a) = 2 * 0(b) &#8658; 0 = 0.<br>

Each time we apply a rule S it gives us:<br>
#a(total) = #(a) + 2<br>
#b(total) = #(b) + 1<br>

Essentially, every time we apply a rule S, we are adding two a's and one b to the number of a's and b's we already to have to get the new total.<br>

Plugging this back into the original formula gives us:<br>

#a = 2 * #b &#8658; <br>
#a + 2 = 2 (#b + 1) &#8658;<br>
#a + 2 = 2#b + 2<br>

Here we can see on the right side we can plug back in our original formula:<br>

#a + 2 = #a + 2<br>

Therefore proving our original claim that all strings produced by the grammar #a = 2#b are valid.<br>

2.) Completeness of this grammar ensures that all valid strings are produced<br>

Base Case: S &#8594; ϵ, meaning that there are 0 a's and 0 b's. Therefore, 0(a) = 2 * 0(b) &#8658; 0 = 0. <br>

Each time we apply a rule S it gives us:<br>
#a(total) = #(a) + 2<br>
#b(total) = #(b) + 1<br>

#a = 2 * #b &#8658; <br>
#a + 2 = 2 (#b + 1) &#8658;<br>
#a + 2 = 2#b + 2<br>

Canceling the two's on each side gives us:<br>

#a = 2#b<br>

Therefore, our original claim that this grammar ensures all valid strings are produced is true. 

### **3.2 Simplicity of Grammar**
The following reasons makes this grammar one of the simplest for the language L:

1) Only utilizes one nonterminal symbol which is S
2) Only 3 recursive productions + ϵ
3) The ratio of exactly 2:1 remains constant throughout every single production made
4) A easy to understand mathemtacial formula is used to prove the theory (a = 2n)
5) Removing any of the three production of strings ("aab", "aba", "baa") can reject the process of generating all valid strings.

For example, removing S &#8594; aSbSaS means we do not have the aba pattern. In simpler terms, we cannot generate a string in L where the b is positioned between 2 a's. Therefore, the grammar is incomplete as it does not allow all three permutations. 

### **4. References**
- Index of /class/archive/cs/cs103/cs103.1164/lectures/18. (2016). Stanford.edu. https://web.stanford.edu/class/archive/cs/cs103/cs103.1164/lectures/18/
- Campbell, R. (2026). Sec 2.1 Context-Free Grammars Lecture slides COMP-382-ON1: Language, Computation and Machines. University of the Fraser Valley‌
- Sipser, M. (2013). Introduction to the theory of computation. Course Technology Cengage Learning.‌
- PageWizard Games, Learning & Entertainment. (2023, May 12). Proving a Context-Free Grammar is Correct (Theory of Computing). YouTube. https://www.youtube.com/watch?v=dOP1ASa6jZg
‌
