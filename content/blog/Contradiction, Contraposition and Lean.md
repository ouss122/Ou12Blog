+++
author = "by Oussama"
title = "Contradiction, Contraposition and Lean"
date = "2025-09-01"
math = true
description = "Deep dive to some methods of proofs and their formalization with lean"
tags = [
    "lean",
    "math",
]
+++


# Introduction

There is nothing better in Math then the joy of proving a theorem but believe me proving it with **Lean** is just another level.

**Lean** is proof assistant programming language (also known as interactive theorem provers ) that help us to write "correct" proofs by : 

- Checking and Pointing out any mistake in our proof
- Giving useful hints and suggestions when needed
- Displaying the current _goal(s)_ (what we need to prove) and our _hypotheses_ (What we know) in real time
- The huge _Mathlib_ library containing thousands of theorems proved by other mathematicians that we can easily use and apply in our proof

You might hear the sentence "formalizing a proof with lean" which mean converting a classic pen and paper proof into a proof written in formal language which is **Lean** in our case


This article is divided in two parts :
- In the first part is a general introduction to proofs where we will prove a simple theorem with different techniques 
- And in the second part we are going to formalize those proofs with lean



# Part One : Introduction to proofs

Our goal is to prove that : for any integer n ( $n\in\mathbb{Z}$ ) :

$$
\text{If }n^2 \text{ is even then } n \text{ is even}
$$

We can also write the proof as the form $P\implies Q$ which is read as "$P$ **_implies_** $Q$" :

$$n^2\text{  is even } \implies n \text{ is even}  $$

Where $P$ is called **_hypothesis_** and $Q$ is called **_conclusion_** or **_consequence_**.

Proving this theorem (or statement) means providing an evidence that no matter the integer n if it is fulfill the **_hypothesis_** which is $n^2$ is even then it must fulfill the **_consequence_** too

Sadly we can't test the theorem for every number because there are an infinite of them, so we have to find another way ...

### A) Direct Proof

In this method we assume $P$ (in other words we have $P$ ) and try to prove $Q$

So we assume that $n^2$ is even and try to prove that $n$ is even
In other words:
We assume $n^2=2k$ and prove that $n=2k'$ where $k,k'\in\mathbb{Z}$ 

We know that $n^2$ is even number (from our _hypothesis_ $P$) and by definition of even number we get:
$$
                          n^2=2*k 
$$
We take the square root of both sides:

$$
n=\sqrt{2*k}
$$

Introducing the square root just make reaching our goal harder, so we should try the next method instead

### B) Proof by Contrapositive

If starting from the $n^2$ element to reach the $n$ element make it harder why can't we start from the $n$ element and climb to the $n^2$ element, and that what "Proof by contrapositive" is about

We have a fact that say if $P\implies Q$ then it is the same as $\neg Q\implies \neg P$ , we call this statement the contrapositive of $P\implies Q$ 

More mathematically we can say that $P\implies Q$ is equivalent to $\neg Q\implies\neg P$ , so instead of proving the first we can prove the second one

That's a lot of information!, let's build it bit by bit :

The $\neg$ symbol mean "the negation" or "the opposite" so if $P$ is True, the negation of $P$ (which is $\neg P$) is False.

Okay now let's take an example to explain that equivalence:


$$
\text{The fuel tank is not empty}\implies\text{the car will move}
$$
now let's write the contrapositive form

$$
\neg\text{ (the car will move)}\implies\neg\text{ (The fuel tank is not empty)}
$$
let's simplify it
$$
\text{ the car doesn't move}\implies\text{ The fuel tank is empty}
$$

........................................................

Okay now after we make everything clear we can prove our theorem :

We have 
$$n^2\text{  is even } \implies n \text{ is even}  $$
By using the contrapositive form
$$n\text{  is odd } \implies n^2 \text{ is odd}  $$
The negation of `n is even` is `n is odd` the same goes for $n^2$

now let's do the same as before we suppose that $n$ is odd and we prove that $n^2$ is odd

By definition of odd number we have :

$$ n=2*k+1 $$
We square both sides
$$n^2=(2*k+1)^2$$
we simplify the right side
$$n^2=4k^2+1+4k$$
by taking 2 as a factor
$$n^2=2(2k^2 +2k)+1$$
let define $k'=2k^2+2k$ 
$$n^2=2k'+1$$
which is the definition of odd number that mean $n^2$ is odd number

Because the contrapositive of $n^2\text{  is even } \implies n \text{ is even}$ is true , $n^2\text{  is even } \implies n \text{ is even}$ is also true
