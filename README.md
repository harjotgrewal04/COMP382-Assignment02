# **COMP 382 - Assignment 2**

## **Group Members: Inder, Sophie, Sahil, Harjot**

## **1. Project Overview**
Given ∑ = {a,b}, find a CFG generating the language L of strings which have twice as many a's as there are b's. The grammar must be proven correct and justified in why it is one of the simplest that could be made for this language L.

## **2. Context-Free Grammar**
A Context-Free Grammar (CFG) is a formal system used to describe the structure of a language. It defines how strings in the language can be generated using variables and substitution rules.

A grammar generates strings starting from a symbol (usually "S"), and substitution rules are applied continously until no more variable symbols are left.

A CFG is defined by a 4-tuple notation:

G = (V, ∑, R, S) where

- V is a finite non-empty set, called the *variables*
- ∑ is a finite set of alphabet or symbols, called the *terminals*
- R is a finite set of *rules* in the form X → y, where X must belong to V and y must be a string in V or ∑
- S is a variable in the set V, also known as the start variable

We call the set of all possible strings derived by a grammar the *language of the grammar*, or L(G).

### **2.1 Example CFG**

Consider the following grammar:

```
E → int          
E → E Op E      
Op → +          
Op → -          
Op → /          
Op → *
```

This grammar generates arithmetic expressions composed of arbitrary integers (int) and the binary operators +, -, *, and /.

Here:

- V = {E, Op}
- ∑ = {int, +, -, *, /}
- S = E

Example derivations:

```
E → int
E → E Op E → int Op E → int + E → int + int
E → E op E → E op E op E → int + int / int
```

The language of the example grammar would be:

```
L = { w ∈ Σ | #int(w) = #Op(w) + 1 }
```

## **3. Solution**
Let G = (V, ∑, R, S) be our grammar, where V = {S}, ∑ = {a, b}, R: {}, and the starting symbol be S.

We can also define the context free language as:

```
L = {w ∈ Σ | #a(w) = 2#b(w)}
```

When looking at the topic, since we need twice as many a's as there are b's, we can consider the number of b's as 'n', which means the number of a's can be described as 2n.

```
b = n
a = 2n
```

For a simple example, let's say we have 1 'b'. Then there would need to be 2 a's.

```
b = 1
a = 2(1) = 2
```

The strings we can make in this case would be "aab", "aba", and "baa".

One attempt at making rules for a CFG was:

```
S → aaSb
S → ε
```

While this does create strings that have twice as many a's as there are b's (e.g. "aab", "aaaabb", "aaaaaabbb"), the issue is that the strings only follow the pattern "aab". These rules do not produce any strings with the other patterns "aba" or "baa", which limits the unique strings that the CFG could produce. 

To fix this, we created two more simple CFG's representing patterns "aba" and "baa":

```
S → baSa
S → ε
```
```
S → abSa
S → ε
```

We can now combine the three CFG's into a singular CFG:

```
S → S₁ | S₂ | S₃
S₁ → aaSb | ε
S₂ → abSa | ε
S₃ → baSa | ε
```

Or more simply:

```
S → aaSb | abSa | baSa | ε
```

This CFG allows for strings to be created with multiple patterns of a's and b's, while also enforcing the requirement of having twice as many a's as there are b's.

### **3.1 Proof**
1.) Soundness of this grammar ensures that all strings produced are valid.

Base Case: S → ε, meaning that there are 0 a's and 0 b's. Therefore, 0(a) = 2 * 0(b) ⟹ 0 = 0.

Each time we apply a rule S it gives us:

```
#a(total) = #(a) + 2
#b(total) = #(b) + 1
```

Essentially, every time we apply a rule S, we are adding two a's and one b to the number of a's and b's we already to have to get the new total.

Plugging this back into the original formula gives us:

```
#a = 2 * #b ⟹
#a + 2 = 2 (#b + 1) ⟹
#a + 2 = 2#b + 2
```

Here we can see on the right side we can plug back in our original formula:

```
#a + 2 = #a + 2
```

Therefore proving our original claim that all strings produced by the grammar #a = 2#b are valid.

2.) Completeness of this grammar ensures that all valid strings are produced.

Base Case: S → ε, meaning that there are 0 a's and 0 b's. Therefore, 0(a) = 2 * 0(b) ⟹ 0 = 0.

Each time we apply a rule S it gives us:

```
#a(total) = #(a) + 2
#b(total) = #(b) + 1
```

```
#a = 2 * #b ⟹
#a + 2 = 2 (#b + 1) ⟹
#a + 2 = 2#b + 2
```

Canceling the two's on each side gives us:

```
#a = 2#b
```

Therefore, our original claim that this grammar ensures all valid strings are produced is true. 

### **3.2 Simplicity of Grammar**
The following reasons makes this grammar one of the simplest for the language L:

1) Only utilizes one nonterminal symbol which is S
2) Only 3 recursive productions + ε
3) The ratio of exactly 2:1 remains constant throughout every single production made
4) A easy to understand mathematical formula is used to prove the theory (a = 2n)
5) Removing any of the three production of strings ("aab", "aba", "baa") can reject the process of generating all valid strings

For example, removing S → abSa means we do not have the aba pattern. In other words, we would not be able to generate a string in L where the b is positioned between 2 a's.

### **4. References**
- Index of /class/archive/cs/cs103/cs103.1164/lectures/18. (2016). Stanford.edu. https://web.stanford.edu/class/archive/cs/cs103/cs103.1164/lectures/18/
- Campbell, R. (2026). Sec 2.1 Context-Free Grammars Lecture slides COMP-382-ON1: Language, Computation and Machines. University of the Fraser Valley‌
- Sipser, M. (2013). Introduction to the theory of computation. Course Technology Cengage Learning.‌
- PageWizard Games, Learning & Entertainment. (2023, May 12). Proving a Context-Free Grammar is Correct (Theory of Computing). YouTube. https://www.youtube.com/watch?v=dOP1ASa6jZg
‌
