# **COMP382-Assignment02**
## **Group Members: Inder, Sophie, Sahil, Harjot**
### **1. Project Overview**
Find a CFG with ∑ = {a,b} and will create the language L and contains strings which will have twice as many a's as there is b's. The grammar must be proven correct and also must be justifiable why it is the simplest that could be made for this language L. 
### **2. Context-Free Grammar**
Context-Free Grammar (CFG) allows us to show languages using using variables together with production rules to convert those variables into alphabet symbols. When a string only has alphabet symbols and no variables that is when we can call it a context-free grammar. 

A CFG is defined by a 4-tuple notation:
G = (V, ∑, R, S)

V is a finite non-empty set which contains the variables
∑ is the set of alphabet or symbols
R is a set of rules where in the form X --> y where X must belong to V and y must be a string in V or ∑
S is a variable in the set V known as the start variable
### **3. Progress**
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

This does create strings that have twice as many a's as there are b's (e.g. "aab", "aaaabb", "aaaaaabbb"), however the issue is that the strings only follow the pattern "aab". These rules do not produce any strings with the other patterns "aba" and "baa", which limits the unique strings that the CFG could produce.

On a side note, if the number of a's and b's is an empty string (), it meets the condition of being a string in L.





