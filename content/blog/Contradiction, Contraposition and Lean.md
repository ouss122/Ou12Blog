+++
author = "by Oussama"
title = "Contradiction, Contraposition and Lean"
date = "2025-09-01"
math = true
description = "Deep dive to some methods of proving theorems with an introduction to Lean theorem prover"
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

The $\neg$ symbol mean "the negation" or "the opposite" so if $P$ is True, the negation of $P$ (which is $\neg P$) is False.

Now let's prove our theorem :

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

We simplify the right side

$$n^2=4k^2+1+4k$$

By taking 2 as a factor

$$n^2=2(2k^2 +2k)+1$$

Let define $k'=2k^2+2k$ 

$$n^2=2k'+1$$

Which is the definition of odd number that mean $n^2$ is odd number

Because the contrapositive of $n^2\text{  is even } \implies n \text{ is even}$ is true , $n^2\text{  is even } \implies n \text{ is even}$ is also true

### C) Proof by Contradiction

Another way to prove a theorem $P$ is by assuming that $\neg P$ is true and then find a contradiction (any result that's obviously false e.g. $0=1$ ) which confirm that $\neg P$ is definitely false so $P$ is true

Let's apply it to our theorem, first we assume that the whole statement is false

$$
\neg (n^2\text{ is even} \implies {n\text{ is even}})
$$

De Morgan Law state that $\neg (P\implies Q)\iff P \land \neg Q$ (the $\iff$ symbol used to show equivalence) ,which turn our statement into:

$$n^2 \text{ is even } \land n \text{ is odd} $$
which is read as $n^2$ is even ***and*** n is odd, now that we have those two assumptions let's try to find a contradiction:

like we did in the "Proof by Contrapostion" section :

$$ n = 2k + 1 $$
$$n^2 = (2k+1)^2$$
$$ n^2 = 4k^2 +1 + 4k$$
$$n^2=2(2k^2+2k)+1$$
Let's define $k'=2k^2+2k$
$$n^2=2k'+1$$

We can see that $n^2$ is an odd number by definition, but our assumption say that $n^2$ is even Contradiction!!!

Which prove that $\neg (n^2\text{ is even} \implies {n\text{ is even}})$ is false so "$n^2\text{ is even} \implies {n\text{ is even}}$" must be true

# Part Two : Formalizing with Lean

### Quick Recap: 

Our goal was to prove that 
$$
n^2\text{ is even} \implies {n\text{ is even}}
$$
which we did using [contrapositive](#b-proof-by-contrapositive) and [contradiction](#c-proof-by-contradiction) methods, Now we will write those two proofs in Lean

To use Lean you can either [install](https://leanprover-community.github.io/get_started.html) it locally or use the [lean4web](https://live.lean-lang.org/#codez=JYWwDg9gTgLgBAWQIYwBYBtgCMBQOCmAHkuOvnAN4B2cAXHICSEAvnABSp1wCiAbvjaxoA9OACYAlOM69+bKuNoBeOFgCeOOHADO0KKqA) online version

For this tutorial we are going to use the [online](https://live.lean-lang.org/#codez=JYWwDg9gTgLgBAWQIYwBYBtgCMBQOCmAHkuOvnAN4B2cAXHICSEAvnABSp1wCiAbvjaxoA9OACYAlOM69+bKuNoBeOFgCeOOHADO0KKqA) version, open the link and you will get this:

![d](/images/a.png)

The left-hand side is where you type the code (or the proof in our case) and the right-hand side is called the **Info view** where Lean will display all the important information (e.g. hypothesis, goals, errors, suggestions, ...)

Now back to the code:
```lean4
import Mathlib
  

example {n : ℤ} (h : Even (n ^ 2)) : Even (n):= by
  sorry
```

The first line tell Lean to import the `Mathlib` library which contain everything we need to prove our theorem.
Note : it's a bad practice to import all the `Mathlib` library you should only import what you need only, I did it to keep the tutorial simple

The 7th line is the one we use to declare a theorem which are going to prove
- The `example` keyword is used to declare that we are going to start a proof, we can also use `theorem` or `lemma` keyword. But unlike `example` you need to provide a name for them that so you can refer to them later in other proofs which is not possible for `example` (e.g. `theorem even_square` or `theorem my_unique_proof` the name doesn't matter)
- `{n : ℤ}` we define an integer n
- `(h : Even (n ^ 2))` we declare the hypothesis (the $P$ from before) which is $n^2$ is even and give it a name (I give the name `h`) so we can refer to it in our proof
- `: Even (n)` now we declare the consequence (the $Q$ from before) which must be typed after the `:`
- `:=` after this symbol we start writing the proof if we have a proof that can directly close our goal ($n$ is even) we can write it after that symbol and we are done (e.g.`:= even_squae_eq_ev` ) . We call this mode **Term mode**

  Note: for trivial theorems we can even use our hypotheses to close the goal
  for example, if want to prove $P$ (any statement $P$) and we already have $P$ as a hypothesis we can do :
```
theorem very_easy  (h : P) : P := h
```

- Okay back to our theorem, in our case we don't have a theorem to close the goal so we switch to **Tactic mode** (where we will use tactics to close the goal) by using the keyword `by` after `:=`

Notice that if you go to the [online](https://live.lean-lang.org/#codez=JYWwDg9gTgLgBAWQIYwBYBtgCMBQOCmAHkuOvnAN4B2cAXHICSEAvnABSp1wCiAbvjaxoA9OACYAlOM69+bKuNoBeOFgCeOOHADO0KKqA) version and put your mouse cursor after the `by` keyword the Info view change 

> **1 goal**
> 
> **n** : ℤ
> 
> **h** : Even (n ^ 2)
> 
> **⊢** Even n

We see everything we defined so far the number `n` , the hypothesis `h` and our goal which is anything after **⊢** .

The 8th line have the keyword `sorry` which mean "sorry we don't have proof yet but please don't throw an error"

Now let's try to prove it using our previous knowledge


### A) Proof by Contradiction

```lean4
import Mathlib

example {n : ℕ} (h : Even (n ^ 2)) : Even (n):= by
  by_contra hneg

```

We start the proof by using `by_contra` tactic which does exactly as we did in the beginning of the contradiction proof. If we have a hypothesis $P$ and consequence $Q$ (or in the form $P\implies Q$) it return a new hypothesis $\neg Q$ and give it the name `hneg` and keep our original hypothesis $P$ . Which we can see in the info view if we put the cursor after `hneg`

> **n** : ℕ
> 
> **h** : Even (n ^ 2)
> 
> **hneg** : ¬Even n
> 
> **⊢** False

Notice that the goal changed to **False** which mean that if we can use our assumptions to find a contradiction that it is obviously false we can close the goal and the theorem is proved

You can also see that our hypothesis `hneg` is $\neg\text{ Even }n$ , Lean doesn't know that the negation of even is odd so we have to use an already proven theorem from the `Mathlib` library that say just that which is `Nat.not_even_iff_odd` : 

```lean4
#check Nat.not_even_iff_odd
```

`#check` let us print the theorem in our info view (putting the cursor at the end of the line or by hovering at `#check`)

> Nat.not_even_iff_odd {n : ℕ} : ¬Even n ↔ Odd n

Notice the equivalence keyword **↔** , what are we going to do next require an implication not equivalence likely there is a way to do a transform

```lean4
#check Nat.not_even_iff_odd.1
```

The `.1` give the left to right implication, which is the one we will use
> Nat.not_even_iff_odd.mp : ¬Even ?m.1 → Odd ?m.1

```lean4
#check Nat.not_even_iff_odd.2
```

And `.2` give the other way around
> Nat.not_even_iff_odd.mpr : Odd ?m.1 → ¬Even ?m.1

Note: you can also read definition of theorem or tactic or any keyword by hovering above it with the mouse

```lean4

apply Nat.not_even_iff_odd.1 at hneg
unfold Odd at hneg
obtain ⟨ k,hk⟩ := hneg

```

- We use the `apply` tactic to apply the implication $\neg\text{ Even }n\implies\text{Odd }n$ to the `hneg` hypothesis which convert it to `Odd n` as you can see in the info view
> **1 goal**
> 
> **n** : ℕ
> 
> **h** : Even (n ^ 2)
> 
> **hneg** : Odd n
> 
> **⊢** False

- `unfold` tactic as the name implies unfold the definition in this case the definition of `Odd` in the hypothesis `hneg` which give the following
> **1 goal**
> 
> **n** : ℕ
> 
> **h** : Even (n ^ 2)
> 
> **hneg** : ∃ k, n = 2 * k + 1
> 
> **⊢** False

   The `∃` keyword mean "there exists" which give the following "there exists a number k that satisfies n = 2 * k + 1".
   Note that the `unfold` tactic only needed for us humans to make the hypothesis more readable, but Lean will do it automatically when using some tactics like `apply`
   
- `obtain` tactic break the hypothesis `hneg` into two hypothesis `h` and `hk`

> **n** : ℕ
> 
> **h** : Even (n ^ 2)
> 
> **k** : ℕ
> 
> **hk** : n = 2 * k + 1
> 
> **⊢** False

```lean4

have h': Odd (n^2) := by

  unfold Odd
   
  use (2*k^2 +2*k)

  calc

    n^2 = (2*k +1)^2       := by rw [hk]

    _ = 2*(2*k^2 +2*k) + 1 := by ring
```

Remember in the proof by contradiction when we proved that $n^2$ is odd we started from the hypothesis n is odd then by definition
$$ n = 2k + 1 $$
$$n^2 = (2k+1)^2$$
$$ n^2 = 4k^2 +1 + 4k$$
$$n^2=2(2k^2+2k)+1$$
Let's define $k'=2k^2+2k$
$$n^2=2k'+1$$
we are going to do exactly the same

- The `have` tactic allow us to introduce new hypothesis but we need to prove it, we introduce the hypothesis `h'` which say $n^2$ is Odd by using the newly obtained hypothesis `hk`.

  If you place the cursor after the `by` keyword you can see that goal change in the info view


> **n** : ℕ
> 
> **h** : Even (n ^ 2)
> 
> **k** : ℕ
> 
> **hk** : n = 2 * k + 1
> 
> **⊢** Odd (n ^ 2)

- Notice that we used the `unfold` tactic without specifying a hypothesis then it will be applied to the goal as you see in the info view 

> ...
> 
> **⊢** ∃ k, n ^ 2 = 2 * k + 1

- The goal now have the ∃ keyword we now have to provide a value that satisfies the `n^2=2*k+1`, we know from the proof we did before that $2k^2+2k$ satisfies it so we use the tactic `use` followed by the value $2k^2+2k$ our goal become
> ...
> 
> **⊢** n ^ 2 = 2 * (2 * k ^ 2 + 2 * k) + 1

- To be able to perform operations on equations (.e.g substitution, simplification, ...) we enter the `calc` mode, in the calc mode every step must be proved 
     - `n^2 = (2*k +1)^2       := by rw [hk]` we start from $n^2$ and then substitute n with it's equivalent `2*k +1` which we know from the hypothesis `hk` .
     - To do this in lean we write the equation`n^2 = (2*k +1)^2` and then add the `:=` to declare that we are going to prove it. Add the `by` keyword to enter tactic mode, notice that the goal changed to **⊢** n ^ 2 = (2 * k + 1) ^ 2
     - We use the tactic `rw` (which stands for rewrite) with the hypothesis `hk` .`rw` will replace the left-hand side of the `hk` found on the left-hand side of our goal with whatever in the right-hand side of `hk` which is exactly our goal
     
     - `_ = 2*(2*k^2 +2*k) + 1` the `_` is equivalent to what was on the right-hand side on the step above which in this case `(2*k +1)^2` so the equation which we need to prove is `(2*k +1)^2= 2*(2*k^2 +2*k) + 1` 
     - We can prove this kind of algebraic simplification easily by using the `ring` tactic as shown in the code above
     - And like that we successfully proved that `n^2 = 2*(2*k^2 +2*k) + 1` which is exactly our goal needed to prove the hypothesis `h'`

Let's see the info view to check our progress put the cursor on newline after the previous code

> **n** : ℕ
> 
> **h** : Even (n ^ 2)
> 
> **k** : ℕ
> 
> **hk** : n = 2 * k + 1
> 
> **h'** : Odd (n ^ 2)
> 
> **⊢** False



