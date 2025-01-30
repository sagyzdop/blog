---
layout: post
title: "Pumping Lemma (for Regular Languages)"
excerpt: "Explanation of the Pumping Lemma with example proof."
date: 2025-01-30 00:01:01 +0500
categories: post
tags:
- regular-languages
- pumping-lemma
- formal-languages
usemathjax: true
---

A formal language that is recognized by a DFA (or NFA, or RegExp) is called a **Regular** language. Some languages would require a DFA with unbounded memory to recognize them, which is not possible. Such languages are **Non-Regular**.

**Pumping Lemma** states that if $L$ is a regular language, then there exists a pumping length $p$ for the language such that for any $w \in L$ where $\lvert w \rvert \ge p$, there is some way we can divide $w$ into parts $x,y,z$ where:

1. $\lvert xy \rvert  \le p$
2. $y\ \text{is not the empty string}$
3. $xy^{i}z \in L, \text{for all}\ i \in \\{0, 1, 2, \dots \\}$

In formal terms we can write this as:

$$
% Original Pumping Lemma
\begin{aligned} 
&\exists p \in \mathbb{N},\ \forall w \in L\ \text{with } \lvert w\rvert  \geq p,\ \exists x,y,z \in \Sigma^* \\ 
&\Bigg( 
\begin{aligned} 
& \lvert xy \rvert  \leq p \\ 
& \land\ \lvert y \rvert  > 0 \\ 
& \land\ \forall i \geq 0\ (xy^i z \in L) 
\end{aligned} 
\Bigg)
\end{aligned} 
$$

> Lemma guarantees that $xy^{i}z$ is in the language but $x, y, z$ separately are just **arbitrary substrings** of $w$, not necessarily strings in $L$. They are simply strings over the alphabet $\Sigma$, so they belong to $\Sigma^*$.

The Pumping Lemma says that:

$$
\text{Regular} \implies \text{Pumpable}
$$

and so:

$$
\text{Not Pumpable} \implies \text{Non-Regular}
$$

But this does **NOT** mean if the language is pumpable – it is regular, i.e. it cannot be used to prove that a language is regular. However, pumping lemma is a tool that can be used to prove that a language is non-regular. We can use the negation of the lemma:

$$
% Negation of Pumping Lemma
\begin{aligned} 
&\forall p \in \mathbb{N},\ \exists w \in L\ \text{with } \lvert w\rvert  \geq p,\ \forall x,y,z \in \Sigma^* \\
&\Bigg( 
\begin{aligned} 
& \lvert xy\rvert  \leq p \\ 
& \land\ \lvert y\rvert  > 0 \\ 
& \implies \exists i \geq 0\ (xy^i z \notin L) 
\end{aligned} 
\Bigg)
\end{aligned} 
$$

Which makes proving that a language is non-regular a question of finding a word that is in the language, but is not pumpable.

## Proof Template

1. Suppose $L$ is pumpable with pumping length $p$.
2. Choose an arbitrary $w \in L$ where $\lvert w\rvert  \ge p$.
3. If we divide up $w$ into $xyz$, where $\lvert xy\rvert  \le p$, and $y$ is **nonempty**, then:
	- *(Give facts about the $xy$ and $z$ that you can infer from the language.)*
4. Thus, both when pumping down by removing $y$, and pumping up by repeating $y$ the pumping lemma must still hold.
5. This means that $xy^{i}z$ should also be in $L$, but it cannot be since it *(give a reason specific to the language)*, so $xy^{i} z \notin L$.
6. Therefore, $L$ cannot be pumpable, and thus cannot be regular.

## Example Proof: $L = \\{a^{n} b^{n}\\}$

1. Suppose $L = \\{a^{n}b^{n}\ \mid\ n \in N\\}$ is pumpable with pumping length $p$.
2. Let $w = a^{p}b^{p}$, which obviously is in $L$.
3. If we divide up $a^{p}b^{p}$ into $xyz$, where $\lvert xy\rvert  \le p$, and $y$ is **nonempty**, then:
	- $x$ and $y$ only contains $a's$
	- Since $\lvert y\rvert  \gt 0$, $y = a^{k}\ \text{and}\ \lvert y\rvert  = k$ for some $1 \le k \le p$
	- $z$ may contain some $a's$, but contains all the $b's$
4. Thus, **pumping down** with $i = 0$:
	- Remove $y$ so that $xz = a^{p−k}b^{p}$
	- The number of $a's$ become $p − k$, while $b's$ remain $p$.
	- Since $k \ge 1$, $p - k \lt p$.
	- Thus $a's \neq b's$, therefore $xz \notin L$
5. And **pumping up** with $i = 2$:
	- Repeat $y$ so that $xy^{2}z = a^{p+k}b^{p}$
	- The number of $a's$ become $p + k$, while $b's$ remain $p$.
	- Since $k \ge 1$, $p + k \gt p$.
	- Thus $a's \neq b's$, therefore $xy^{2}z \notin L$
6. Therefore, $L$ cannot be pumpable, and thus cannot be regular.

### Pumping down with $y^{0}$ nuance

One thing I was confused about when understanding the proof was the pumping down part.

> Isn't it stated in the lemma that $y$ must be non-empty, so how come we remove the $y$ part and claim that language is non-regular?

The Pumping Lemma requires that **for any valid $w=xyz$ split** $y$ has to be non-empty **only in the original split**. Pumping down ($i=0$) removes $y$, producing $xz$. The lemma guarantees nothing about the new string $xz$ containing $y$; it only requires $xy^{0}z \in L$. So everything checks out. Non-empty $y$ applies only to the word that we choose initially, but pumping down allows us to remove it, and it still has to be in the language.

---

> Note that pumping lemma has no utility for finite languages, since we can pick $p$ greater than the size of the language which makes the lemma vacuously true. Besides, a finite language is regular by definition, since it is possible to construct a DFA (or NFA, or RegExp) that recognizes all the words in it. And since the lemma can be used to only prove non-regularity of a language it is useless in this case.
 