# **COMP382-Assignment02**
## **Group Members: Inder, Sophie, Sahil, Harjot**
### **1. Project Overview**
Let 𝛴 = {a, b}. Give a CFG generating the language L of strings with twice as many a's as b's. Prove that your grammar is correct. Also give an argument to justify why your grammar is one of the simplest that can be designed to recognize this language L.
### **2. Context-Free Grammar**
Context-Free Grammar (CFG) allows us to show languages using using variables together with production rules to convert those variables into alphabet symbols. When a string only has alphabet symbols and no variables that is when we can call it a context-free grammar. 

A CFG is defined by a 4-tuple notation:
G = (V, ∑, R, S)

V is a finite non-empty set which contains the variables
∑ is the set of alphabet or symbols
R is a set of rules where in the form X --> y where X must belong to V and y must be a string in V or ∑
S is a variable in the set V known as the start variable
