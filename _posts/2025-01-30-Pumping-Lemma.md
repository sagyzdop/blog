---
layout: post
title: "Pumping Lemma (for Regular Languages)"
excerpt: "Explanation of the Pumping Lemma with example proof."
date: 2025-01-20 01:01:01 +0500
categories: post
tags:
- regular-languages
- pumping-lemma
- formal-languages
usemathjax: true
---

Pumping lemma states that if $L$ is a regular language, then there exists a pumping length $p$ for the language such that for any $w \in L$ where $|w| \ge p$, there is some way we can divide $w$ into parts $x,y,z$ where:

1. $|xy| \le p$
2. $y\ \text{is not the empty string}$
3. $xy^{i}z \in L, \text{for all}\ i \in \{0, 1, 2, \dots \}$

In formal terms we can write this as :

$$
% Original Pumping Lemma
\exists p \in \mathbb{N},\ \forall w \in L\ \text{with } |w| \geq p,\ \exists x,y,z \in \Sigma^* \ \Bigg( 
\begin{aligned} 
& |xy| \leq p \\ 
& \land\ |y| > 0 \\ 
& \land\ \forall i \geq 0\ (xy^i z \in L) 
\end{aligned} 
\Bigg)
$$

> Lemma guarantees that $xy^{i}z$ is in the language but $x, y, z$ are just **arbitrary substrings** of $w$, not necessarily strings in $L$. They are simply strings over the alphabet $\Sigma$, so they belong to $\Sigma^*$.

The Pumping Lemma says that:

$$
\text{Regular} \implies \text{Pumpable}
$$

and so:

$$
\text{Not Pumpable} \implies \text{Non-Regular}
$$

but this does **NOT** mean if the language is pumpable it is regular. Pumping Lemma is a tool that can be used to show that some languages are not regular. However, it cannot be used to show that a language is regular. However, we can use the negation of the statement to prove that the language is non-regular. Negating the statement we get:

$$
% Negation of Pumping Lemma
\forall p \in \mathbb{N},\ \exists w \in L\ \text{with } |w| \geq p,\ \forall x,y,z \in \Sigma^* \ \Bigg( 
\begin{aligned} 
& |xy| \leq p \\ 
& \land\ |y| > 0 \\ 
& \implies \exists i \geq 0\ (xy^i z \notin L) 
\end{aligned} 
\Bigg)
$$

Which makes proving that a language is irregular a question of finding a word that is in the language, but that is not pumpable.

## Proof Template

1. Suppose $L$ is pumpable with pumping length $p$.
2. Choose an arbitrary $w \in L$ where $|w| \ge p$.
3. If we divide up $w$ into $xyz$, where $|xy| \le p$, and $y$ is **nonempty**, then:
	1. *Give facts about the $xy$ and $z$ that you can infer from the language.*
4. Thus, both when pumping down by removing $y$, and pumping up by repeating $y$ the pumping lemma must still hold.
5. This means that $xy^{i}z$ should also be in $L$, but it cannot be since it *(give a reason specific to the language)*, so $xy^{i} z \notin L$.
6. Therefore, $L$ cannot be pumpable, and thus cannot be regular.

## Example Proof:  $\{a^{n} b^{n}\}$

1. Suppose $L = \{a^{n}b^{n}\ |\ n \in N\}$ is pumpable with pumping length $p$.
2. Let $w = a^{p}b^{p}$, which obviously is in $L$.
3. If we divide up $a^{p}b^{p}$ into $xyz$, where $|xy| \le p$, and $y$ is **nonempty**, then:
	1. $x$ and $y$ only contains $a's$
	2. Since $|y| \ge 0$, $y = a^{k}\ \text{and}\ |y| = k$ for some $1 \le k \le p$
	3. $z$ may contain some $a's$, but contains all the $b's$
4. Thus, pumping down with $i = 0$:
	1. Remove $y$: $xz = a^{p−k}b^{p}$
	2. The number of $a's$ becomes $p − k$, while $b's$ remain $p$.
	3. Since $k \ge 1$, $p - k \lt p$.
	4. Thus $a's \neq b's$, therefore $xz \notin L$
5. And pumping up with $i = 2$:
	1. Repeat $y$: $xy^{2}z = a^{p+k}b^{p}$
	2. The number of $a's$ becomes $p + k$, while $b's$ remain $p$.
	3. Since $k \ge 1$, $p + k \gt p$.
	4. Thus $a's \neq b's$, therefore $xy^{2}z \notin L$
6. Therefore, $L$ cannot be pumpable, and thus cannot be regular.

> Note that pumping lemma has no utility for finite languages, since we can pick $p$ greater than the size of the language which makes the lemma vacuously true. Besides, finite a language is regular by definition, since it is possible to construct a DFA (or NFA, or RegExp) that recognizes all the words in it. And since the lemma can be used to only prove non-regularity of a language it is useless in this case.
 