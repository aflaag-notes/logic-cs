---
theme: beam
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---

<!-- _class: title -->

# Propositional Dynamic Logic

Mathematical Logic for Computer Science
Alessio Bandiera
1985878

---

# Contents

- **PDL**
- Syntax
- Axiomatization
- Soundness and Completeness
- Complexity
- Variants

---

# PDL

# Dynamic Logics

**Dynamic Logics** are modal logics for representing states and events of dynamic systems

The first DL system was developed in 1976 by Vaughan Pratt, early pioneer of CS. His original DL was a _first-order_ modal logic, and **Propositional Dynamic Logic** (PDL) is the propositional counterpart of it

Being propositional, its only two syntactic categories are **propositions** and **programs**, and _possibility_ and _necessity_ are expressed through modal operators that also indicate the programs they are referring to

- $\langle \pi \rangle \phi$ is read "there is an execution of $\pi$ that ends in a state in which $\phi$ is true"
- $[\pi] \psi$ is read "all executions of the program $\pi$ end in states in which $\psi$ is true"

---

# Contents

- PDL
- **Syntax**
- Axiomatization
- Soundness and Completeness
- Complexity
- Variants

---

# Syntax

# Formulas

Given $\Phi_0$ the set of _atomic formulas_, for any $\phi, \psi \in \Phi_0$
- $\phi \in \mathrm{Form}(\Phi_0)$
- $\lnot \phi \in \mathrm{Form}(\Phi_0)$
- $\phi \lor \psi \in \mathrm{Form}(\Phi_0)$
- $[\alpha] \phi \in \mathrm{Form}(\Phi_0)$

where $\alpha \in \mathrm{Prog}(\Pi_0)$

---

# Syntax

# Programs

Given $\Pi_0$ the set of _atomic programs_, for any $\alpha, \beta \in \Pi_0$

- $\alpha \in \mathrm{Prog}(\Pi_0)$
- $(\alpha; \beta) \in \mathrm{Prog}(\Pi_0)$
- $(\alpha \cup \beta) \in \mathrm{Prog}(\Pi_0)$
- $\alpha^* \in \mathrm{Prog}(\Pi_0)$
- $\phi? \in \mathrm{Prog}(\Pi_0)$

where $\phi \in \mathrm{Form}(\Phi_0)$

---

# Syntax

# Relations

$$(x, y) \in R(\pi) \iff x \stackrel{\pi}{\to} y$$

- $(x, y) \in R(\alpha; \beta) \iff \exists z \in W \quad (x, z) \in R(\alpha) \land (z, y) \in R(\beta)$
- $(x, y) \in R(\alpha \cup \beta) \iff (x, y) \in R(\alpha) \cup R(\beta)$
- $(x, y) \in R(\alpha^*) \iff \exists z_0, \ldots, z_n \in W \quad \left \{\begin{array}{l}z_0 = x \\ z_n = y \\ (z_{k - 1}, z_k) \in R(\alpha) \end{array}\right.$
- $(x, y) \in R(\phi?) \iff x = y \land y \in V(\phi)$

---

# Syntax

# Valuations

$$x \in V(p) \iff p \ \mbox{is true at} \ x$$

- $V(\bot) = \varnothing$
- $V(\top) = W$
- $V(\lnot \phi) = W - V(\phi)$
- $V(\phi \lor \psi) = V(\phi) \cup V(\psi)$
- $V([\alpha] \phi) = \{x \mid \forall y \in W \quad (x, y) \in R(\alpha) \implies y \in V(\phi)\}$

---

<style>
img.left-center {
    position: absolute;
    left: 2em;
    top: 50%;
    transform: translateY(-40%);
    height: 500px;
}
</style>

# LTS

 <img src="../assets/model.svg" class="left-center"/> 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $W = \{y_1, y_2, y_3, y_4\}$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $R(\pi_1) = \{(y_1, y_2), (y_2, y_2)\}$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $R(\pi_2) = \{(y_1, y_3), (y_2, y_4)\}$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $V(p) = \{y_1, y_2\}$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $V(q) = \{y_3, y_4\}$

---

<style>
img.left-center {
    position: absolute;
    left: 2em;
    top: 50%;
    transform: translateY(-40%);
    height: 500px;
}
</style>

# LTS

 <img src="../assets/model.svg" class="left-center"/> 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $\mathfrak M, y_1 \models \left\langle\pi_1^*; \pi_2 \right \rangle q$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $\mathfrak M, y_2 \models \left[\pi_1^*\right]p$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $\mathfrak M, y_1 \models \left [ \pi_1 \cup \pi_2 \right ] (p \lor q)$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; • $\mathfrak M, y_3 \models \left [ \pi_1 \cup \pi_2 \right ] \bot$

---

# Contents

- PDL
- Syntax
- **Axiomatization**
- Soundness and Completeness
- Complexity
- Variants

---

# Axiomatization

# Goal

The goal is to define a **deducibility predicate** $\vdash$ such that
$\vdash$-deductions are both _sound_ and _complete_ in terms of _validity_, i.e. for any $\phi$ it holds that

$$\vdash \phi \iff \models \phi$$

where $\models \phi$ means that $\phi$ is **valid**

---

# Axiomatization

# Validity

We write $\mathfrak M, w \models \phi$ if and only if $w \in V(\phi)$

$\phi$ is _valid_ in $\mathfrak M$, written as $\mathfrak M \models \phi$, if and only if

$$\mathfrak M \models \phi \iff \forall w \in W \quad \mathfrak M, w \models \phi$$

$\phi$ is **valid**, written as $\models \phi$, if and only if

$$\models \phi \iff \forall \mathfrak M \quad \mathfrak M \models \phi$$

---

# Axiomatization

# K and N axioms

$$
    \begin{equation*}
        \begin{alignedat}{2}
            (\mbox K) & \quad \quad && [\alpha] (\phi \to \psi) \to ([\alpha] \phi \to [\alpha] \psi) \\
            (\mbox N) & \quad \quad && \dfrac{\phi}{[\pi] \phi} \\
        \end{alignedat}
    \end{equation*}
$$

A modal logic is **normal** if it obeys $(\mbox K)$ and $(\mbox N)$

---

# Axiomatization

# PDL axioms

PDL is the _least normal_ modal logic containing every instance of

$$
    \begin{equation*}
        \begin{alignedat}{2}
            (\mbox A 1) & \quad \quad && [\alpha ; \beta] \phi \leftrightarrow [ \alpha ] [\beta] \phi \\
            (\mbox A 2) & \quad \quad && [\alpha \cup \beta] \phi \leftrightarrow [ \alpha] \phi \land [\beta] \phi \\
            (\mbox A 3) & \quad \quad && [\alpha ^*] \phi \leftrightarrow \phi \land [\alpha] [\alpha ^*] \phi \\
            (\mbox A 4) & \quad \quad && [\phi?] \psi \leftrightarrow (\phi \to \psi) \\
        \end{alignedat}
    \end{equation*}
$$

and closed under the _loop invariance_ rule of inference

$$(\mbox I) \quad \quad \dfrac{\phi \to [\alpha] \phi}{\phi \to [\alpha^*] \phi}$$

---

# Axiomatization

# $\vdash$-deducibility

A formula $\phi$ is $\vdash$-_deducible_ from $\Sigma \subseteq \mathrm{Form}(\Phi_0)$ if there exists a sequence $\phi_0, \ldots, \phi_n$ such that $\phi_n = \phi$, and for all $i \in [n]$

- $\phi_i$ is an instance of an axiom schema
- $\phi_i$ is an instance of a formula of $\Sigma$
- $\phi_i$ comes from earlier formulas of the sequence by inference

Are $\vdash$-deductions sound and complete?

---

# Contents

- PDL
- Syntax
- Axiomatization
- **Soundness and Completeness**
- Complexity
- Variants

---

# Soundness and Completeness

# Segerberg's axioms

In 1977 Segerberg proposed to replace

$$(\mbox I) \quad \quad \dfrac{\phi \to [\alpha] \phi}{\phi \to [\alpha^*] \phi}$$

with the following fifth axiom

$$(\mbox A 5) \quad \quad \phi \land [\alpha^*] (\phi \to [\alpha] \phi) \to [\alpha^*]\phi$$

in order to prove that such axiomatization was sound and complete

---

# Soundness and Completeness

# Segerberg's axioms

Indeed, it is easy to prove that $(\mbox I)$ can be replaced with $(\mbox A 5)$

$$
    \begin{equation*}
        \begin{alignedat}{2}
            1. \vdash & \ \phi \to [\alpha] \phi && \quad \quad \mbox{(premise)} \\
            2. \vdash & \ [\alpha ^*](\phi \to [\alpha] \phi) && \quad \quad \mbox{(from 1 using (N) with } \pi = \alpha^*) \\
            3. \vdash & \ \phi \land [\alpha ^*] (\phi \to [\alpha] \phi) \to [\alpha^*] \phi && \quad \quad (\mbox A 5) \\
            4. \vdash & \ [\alpha^*](\phi \to [\alpha] \phi) \to (\phi \to [\alpha^*] \phi) && \quad \quad (\mbox{from 3 through prop. reasoning}) \\
            5. \vdash & \ \phi \to [\alpha^*] \phi && \quad \quad (\mbox{from 2 and 4 using \textit{Modus Ponens}})
        \end{alignedat}
    \end{equation*}
$$

---

# Soundness and Completeness

# Soundness

To prove that $\vdash$ is sound w.r.t. $\models$, i.e. that

$$\vdash \phi \implies \models \phi$$

a proof by induction on the length of $\phi$'s deduction in $\vdash$ suffices

So, what about completeness? It requires to prove that

$$\models \phi \implies \vdash \phi$$

---

# Soundness and Completeness

# Completeness

Segerberg's work was the first attempt to prove the completeness of $\vdash$, however in 1978 he found a flaw in his argument

Then in the same year Parikh published what is now considered the first proof of the completeness of $\vdash$

<!-- --- -->
<!---->
<!-- # Soundness and Completeness - Goldblatt -->
<!---->
<!-- Since then, different alternative proof theories of PDL have also been sought after. For example, in 1992 Goldblatt proposed the -->
<!-- $\vdash'$-deducibility predicate, which is based on the same first four axiom schemas along with this _infinitary_ rule of inference -->
<!---->
<!-- $$(\mbox I') \quad \quad \dfrac{ \{[\beta] [\alpha^n] \phi \mid n \in \mathbb N \}}{[\beta] [\alpha^*] \phi}$$ -->
<!---->
<!-- Goldblatt was able to prove that $\vdash'$ is both sound and complete. -->

---

# Contents

- PDL
- Syntax
- Axiomatization
- Soundness and Completeness
- **Complexity**
- Variants

---

# Complexity

# PDL satisfiability

$\phi$ is _satisfiable_ in $\mathfrak M$ if there is a world $w \in W$ such that $\mathfrak M , w \models \phi$

$\phi$ is **satisfiable** if there is a model $\mathfrak M$ such that $\phi$ is satisfiable in $\mathfrak M$

$$\mbox{PDL-SAT} := \{\langle \phi \rangle \mid \phi \ \mbox{is a satisfiable PDL formula}\}$$

---

# Complexity

# Unsatisfiable formulas

$\phi$ is _unsatisfiable_ if and only if $\lnot \phi$ is _valid_

Therefore, we can use the recursive definition of valid PDL formulas and build a procedure $P$ that enumerates all the $\vdash$-deducible formulas

Hence, given enough time if $\lnot \phi$ is $\vdash$-deducible $P$ will eventually find it and determine that $\phi$ is _unsatisfiable_

This proves that $\mbox{PDL-SAT} \in \textsf{coREC}$

---

# Complexity 

# Satisfiable formulas

However, if $\phi$ is satisfiable $P$ never terminates.

Nonetheless, we can leverage the **finite model property** of PDL

$$\forall \phi \in \mathrm{Form}(\Phi_0) \quad \langle \phi \rangle \in \mbox{PDL-SAT} \implies \exists \mathfrak M_{fin} \ \mbox{finite} \quad \phi \ \mbox{satisfiable in} \ \mathfrak M_{fin}$$

Therefore, there is a procedure $P'$ that enumerates all the finite models $\mathfrak M_{fin}$ and checks for each model if $\phi$ is satisfiable in $\mathfrak M_{fin}$

Thus, $P$ and $P'$ can be run in parallel to decide $\mbox{PDL-SAT}$. However, this is _very_ inefficient, can we do any better?

---

# Complexity

# Small model property

Kozen and Parikh proved that PDL has also the **small model property**

$$\forall \phi \in \mathrm{Form}(\Phi_0) \quad \langle \phi \rangle \in \mbox{PDL-SAT} \implies \exists \mathfrak M_{fin} \ \mbox{finite} \quad \left \{ \begin{array}{l} |\mathfrak M_{fin}| < \mathrm{exp}(|\phi|) \\ \phi \ \mbox{satisfiable in} \ \mathfrak M_{fin} \end{array} \right.$$

This property implies that we can stop $P'$ as soon as all the "small" models have been exhausted, to conclude that $\phi$ is not satisfiable

This concludes that $\mbox{PDL-SAT} \in \textsf{NEXP}$. In 1980 Pratt was able to prove that $\mbox{PDL-SAT} \in \textsf{EXP}\mbox{-complete}$

---

# Contents

- PDL
- Syntax
- Axiomatization
- Soundness and Completeness
- Complexity
- **Variants**

---

# Variants

- Variants
    - **Test-free PDL**
    - CPDL
    - IPDL

---

# Test-free PDL

# Expressive power

The "$?$" operator seems _different_ with respect to the other programs, can we remove this operator from PDL?

Let $\mbox{PDL}_0$ be the test-free version of PDL. In 1981 Berman and Paterson proved that this PDL formula

<!-- $$\left \langle (\phi?; \pi)^*; \lnot \phi ? ; \pi; \phi ? \right \rangle \top$$ -->

$$\langle (P?; A)^* ; \lnot P ? ; A; P ? \rangle \top$$

has no $\mbox{PDL}_0$ equivalent formula

<!-- has no $\mbox{PDL}_0$ equivalent formula. This formula can be rewritten as -->

<!-- $$\left \langle \mbox{while} \ \phi \ \mbox{do} \ \pi \right \rangle \langle \pi \rangle \phi$$ -->

---

# Test-free PDL

# Ultimate periodicity

The idea of their counterexample is based on this result in the theory of context-free languages:

A _unary language_ $L = \{1^n \mid n \in \mathbb N\}$ is _regular_ if and only if the set $S = \{n \in \mathbb N \mid 1^n \in L\}$ is _ultimately periodic_

A set $S \subseteq \mathbb N$ is **ultimately periodic** if there are integers $X \in \mathbb N$ and $Y > 0$ such that

$$\forall k \ge X \quad k \in S \iff k + Y \in S$$

For instance, this set $S$ is ultimately periodic

$$S = \{0, 1, 2, 4, 6\} \cup \{k \ge 8 \mid k \equiv 0, 2 \; (\mbox{mod} \; 3)\} = \{0, 1, 2, 4, 6, 8, 9, 11, 12, 14, 15, \ldots\}$$

since it holds that $\forall k \ge 7 \quad k \in S \iff k + 3 \in S$

---

# Test-free PDL

# Ultimate periodicity

A _unary language_ $L = \{1^n \mid n \in \mathbb N\}$ is _regular_ if and only if the set $S = \{n \in \mathbb N \mid 1^n \in L\}$ is _ultimately periodic_

- $\Longrightarrow )$:
  - if $L$ is regular, there is a DFA $D = (Q, \{1\}, \delta, q_0, F)$ that recognizes $L$
  - consider any string $w = 1^n \in L$
  - if $n > |Q|$ then when $D$ reads $w$ some states must repeat by the **pigeonhole principle**
  - hence the set $S = \{n \in \mathbb N \mid 1^n \in L\}$ of the lengths of the strings of $L$ must be _ultimately periodic_

---

# Test-free PDL

# Ultimate periodicity

A _unary language_ $L = \{1^n \mid n \in \mathbb N\}$ is _regular_ if and only if the set $S = \{n \in \mathbb N \mid 1^n \in L\}$ is _ultimately periodic_

- $\Longleftarrow )$: Construct the following DFA $D = (Q, \{1\}, \delta, q_0, F)$
  - $Q = \{q_0, \ldots, q_{X + Y - 1}\}$
  - $\forall i \in [0, X + Y - 1] \quad \delta(q_i, 1) = \left \{\begin{array}{ll}q_{i + 1} & i < X + Y - 2 \\ q_X & i = X + Y - 1\end{array}\right .$
  - $F = \{q_i \mid i < X \land i \in S\} \cup \{q_{X + r} \mid r \in [0, Y - 1] \land X + r \in S\}$

---

# Test-free PDL

# Ultimate periodicity

A _unary language_ $L = \{1^n \mid n \in \mathbb N\}$ is _regular_ if and only if the set $S = \{n \in \mathbb N \mid 1^n \in L\}$ is _ultimately periodic_

- $\Longleftarrow )$: For instance, when

$$S = \{0, 1, 2, 4, 6, 8, 9, 11, 12, 14, 15, \ldots\}$$

we construct the following DFA

<div style="text-align: center;">
    <img src="../assets/up.svg" style="height: 100px;"/>
</div>

---

# Test-free PDL

# Ultimate periodicity

By removing tests from PDL formulas, programs are restricted to regular expressions

Hence, Berman and Paterson built a family of models $\mathfrak A_m$ for $m \ge 2$ in which the only program present is $A$

Therefore, by ultimate periodicity each program over $\mathfrak A_m$ can be rewritten as a regex ending in $\left (A^Y \right)^*$ for some $Y > 0$

---

# Test-free PDL

# The counterexample

<div style="text-align: center;">
    <img src="../assets/Am.svg" style="height: 175px;"/>
</div>

Each $\mathfrak A_m$ consists of $2m + 1$ worlds, where $2m + 1$ is _prime_

This forces $\left (A^Y \right)^*$ to generate all the possible residues modulo $2m + 1$, i.e. each world will be able to reach any other world

Hence, test-free PDL formulas _cannot distinguish_ the worlds in which we are performing the evaluation

---

# Test-free PDL

# The counterexample

<div style="text-align: center;">
    <img src="../assets/Am.svg" style="height: 175px;"/>
</div>

However, tests _can_ distinguish the worlds by building programs which **depend on the truthness of propositions**

$$\langle (P?; A)^* ; \lnot P ? ; A; P ? \rangle \top$$

In fact, this formula is satisfied at $w_0$ but not satisfied at $w_m$

---

# Variants

- Variants
    - Test-free PDL
    - **CPDL**
    - IPDL

---

# CPDL

# The converse operator

CPDL is a variant which adds the **converse** operator to PDL programs

$$(x, y) \in R \left(\alpha^{-1} \right) \iff (y, x) \in R(\alpha)$$

To get a sound a complete system, two additional axioms are needed

$$
    \begin{equation*}
        \begin{alignedat}{2}
            (\mbox A 6) & \quad \quad && \phi \to [ \alpha] \left \langle \alpha^{-1} \right \rangle \phi \\
            (\mbox A 7) & \quad \quad && \phi \to \left [ \alpha ^{-1} \right ] \langle \alpha \rangle \phi \\
        \end{alignedat}
    \end{equation*}
$$

As for PDL, CPDL has the **small model property** too, and $\mbox{CPDL-SAT} \in \textsf{EXP}\mbox{-complete}$ as well

---

<style>
table {
    margin: 0 auto;
}
</style>

# CPDL

# Expressive power

What about the expressive power? Consider these two models

$$\mathfrak M = (W, R, V) \quad \quad \quad \mathfrak M' = (W', R', V')$$

<div style="height: 50px;"></div>

| $\mathfrak M$               | $\mathfrak M'$                |
|-----------------------------|-------------------------------|
| $W = \{x, y\}$              | $W' = \{y'\}$                 |
| $R(\pi) = \{(x, y)\}$       | $R'(\pi) = \varnothing$       |
| $V(x) = V(y) = \varnothing$ | $V'(y') = \varnothing$        |

---

<style>
table {
    margin: 0 auto;
}
</style>

# CPDL

# Expressive power

<div style="height: 30px;"></div>

| $\mathfrak M$               | $\mathfrak M'$                |
|-----------------------------|-------------------------------|
| $W = \{x, y\}$              | $W' = \{y'\}$                 |
| $R(\pi) = \{(x, y)\}$       | $R'(\pi) = \varnothing$       |
| $V(x) = V(y) = \varnothing$ | $V'(y') = \varnothing$        |

<div style="height: 40px;"></div>

From the perspective of PDL $y$ and $y'$ are _indistinguishable_, in fact

$$\mathfrak M, y \models \phi \iff \mathfrak M', y' \models \phi$$

---

<style>
table {
    margin: 0 auto;
}
</style>

# CPDL

# Expressive power

<!-- <div style="height: 15px;"></div> -->

| $\mathfrak M$               | $\mathfrak M'$                |
|-----------------------------|-------------------------------|
| $W = \{x, y\}$              | $W' = \{y'\}$                 |
| $R(\pi) = \{(x, y)\}$       | $R'(\pi) = \varnothing$       |
| $V(x) = V(y) = \varnothing$ | $V'(y') = \varnothing$        |

<div style="height: 40px;"></div>

However CPDL _can_ distinguish $y$ and $y'$ because

$$\mathfrak M, y \models \left \langle \pi^{-1} \right \rangle \top \quad \quad \quad \mathfrak M', y' \not\models \left \langle \pi^{-1} \right \rangle \top$$

meaning that CPDL has **more expressive power** than PDL

---

# Variants

- Variants
    - Test-free PDL
    - CPDL
    - **IPDL**

---

# IPDL

# The intersection operator

IPDL is a variant which adds the **intersection** operator to PDL programs

$$(x, y) \in R(\alpha \cap \beta) \iff (x, y) \in R(\alpha) \cap R(\beta)$$

We observe that

$$\models \left \langle \alpha \cap \beta \right \rangle \phi \to \langle \alpha \rangle \phi \land \langle \beta \rangle \phi$$

but the opposite is not true in general, for instance if $\mathfrak M = (W, R, V)$ is such that

- $W = \{s, t_1, t_2\}$
- $R(\alpha) = \{(s, t_1)\}$
- $R(\beta) = \{(s, t_2)\}$
- $V(\phi) = \{t_1, t_2\}$

---

# IPDL

# Axiomatization and Complexity

Differently from PDL and CPDL, the **axiomatization** of IDPL is *much harder* and has been an open problem until 2003, when Balbiani and Vakarelov presented a *sound* and *complete* proof system of IPDL

Finally, in 2005 Lange and Lutz proved that $\mbox{IPDL-SAT} \in \textsf{2EXP-complete}$

---

<!-- _class: title -->

# Thanks for your attention

Mathematical Logic for Computer Science
Alessio Bandiera
1985878
