---
title: Notes on Knowledge Representation and Reasoning (KRR)
author: Mack Sweeney
layout: post
---

Many of the interesting problems in artificial intelligence (AI) seek to solve
problems using some generalized approach which can be applied to different
knowledge sets to provide answers for a variety of problems. Perhaps the first
example of such a program was Newell and Simon's General Problem Solver (GPS).
More recent programs have sought to address the limitations of GPS in various
ways, but almost all these programs have in common one essential characteristic:
they require a knowledge base (KB) to solve a problem. This is where knowledge
representation comes into play. How does one present knowledge in such a way
that a computer can understand it? This post discusses knowledge representation
and reasoning (KRR) in some detail.

<!--more-->

## Overview (ToC)

1.  History
2.  The Predicate Calculus
    1.  Formal Logic
    2.  The Propositional Calculus
    3.  The Predicate Calculus
        1. First-Order Predicate Calculus (FOPC)
        2. Higher-Order Predicate Calculus (HOPC)
        3. Modal Logic
        4. Set Theory
3.  Logic Programming Languages
    1.  Prolog
    2.  CycL

## History

*   1963: Newell & Simon publish their paper on the GPS.
*   1960s: Most of AI concerned with search techniques and theorem proving.
*   1970s: Expert-system approach emphasizes importance of having the right
    knowledge over having a clever algorithm (shifting focus).
*   1980s: Complexity analysis revealed that most knowledge representation
    languages had worst-case queries which were intractable (exponential, or
    NP-hard).
*   1990s: Focus shifts to knowledge representation _and reasoning_; the goal
    becomes one of balance: find a language which is both efficient in the
    average case and expressive enough to represent most problems.

## The Predicate Calculus

Predicate calculus is the formal language used for knowledge representation. It
is based on formal logic and propositional calculus, and can be divided into
first-order and higher-order varieties. It is also heavily influenced by set
theory and concepts of modal logic. Some prominent languages which allow logic
programming using predicate logic as a foundation are Prolog and CycL (encodes
the Cyc KB).

### Formal Logic

A discipline in which _propositions_ are used in _deductive_ arguments to prove
further propositions. Formal logic is considered an _a priori_ (rather than
empirical) discipline. Some consider it a sub-discipline of mathematics, while
others consider it a closely related but distinct field. It is not: (1) the
study of the _processes_ of reasoning (psychology) or (2) the study of debate or
the art of persuasion.

1.  **proposition/assertion**: an assertively used statement of fact
2.  **deduction**: a rigorous proof/derivation of a proposition from one or
    mother others. In a deduction, the proposition(s) _deduced_ are the
    _conclusion(s)_, while the starting proposition(s) are the _premises_.
    * the _conclusion_ (singular) may also be considered the set of propositions
      derived by the deduction, rather than considering each a conclusion.
    * deductive reasoning often involves a chain of propositions, starting from
      those fundamentally given and proceeding through a chain of sub-problem
      deductions; the chain concludes at some final set of propositions, which
      is the ultimate conclusion. Each individual deduction is linked to the
      next if any of its conclusions are used as a premise in the next.
3.  **a priori**: knowledge that is independent of all particular experiences
    * derives from the latin _a priori_, meaning "from what is before"
    * in contrast to _a posteriori_, meaning "from what is after"

#### A Deductive Argument

A _valid_ deductive argument uses a chain of _inference_ to conclude true
propositions. A _sound_ deductive argument is both valid and starts from _true_
premises.

1.  **inconsistent**: Self-contradictory -- two propositions are inconsistent if
    one contradicts the other. A set of propositions is inconsistent if it
    contains any two such propositions.
2.  **necessity**: A set of propositions follows from another set of
    propositions if it would be _inconsistent_ not to.
3.  **validity**: A deductive argument is valid only if its conclusions are
    necessitated by its premises.
4.  **sound**: A deductive argument is sound if it meets two conditions:
    1.  the deduction is valid
    2.  the premises are true
5.  **truth**: The conclusion of a deductive argument is true if it is a _sound_
    argument.
6.  **inference**: derivation of conclusions from premises by any _acceptable_
    form of reasoning. Deduction is one type of inference. Three others are
    _induction_, _probability_, and _statistical reasoning_.
    * **acceptable**: An acceptable form of reasoning is any which preserves
    truth; in other words, it provides a _valid_ argument.
7.  **induction**: Traditionally considered a type of inference in formal logic,
    induction is now viewed as the domain of the natural sciences, where an
    inductive argument is one which reasons about particular facts to propose
    more general conclusions; this is the method used to formulate theories.

#### Deductive Inference

Deductive inference employs propositional forms to derive conclusions from
premises. Since all inference forms can be expressed as propositional forms,
formal logic can accurately be regarded as the study of propositional forms.

1.  **inference form/rule**: A formula for a statement whose truth is dependent
    on the values of its _variables_.
    * Example: Every X is a Y. Some Z's are X's. Therefore: Some Z's are Y's.
2.  **variables**: Symbols used to denote a position in an inference form into
    which an _expression_ may be insertion. Variable substitution (insertion)
    must be _uniform_ to produce an _instance_ of the form.
    * **uniform**: Substitute same expression for same variable for all
      instances of a variable in an inference rule.
    * **instance**: An expression resulting from the _uniform_ substitution of
      variables.
3.  **proposition(al) form**: An expression whose instances are individual
    propositions rather than inferences from several propositions.
    * **valid**: A valid proposition form has only true instances.
4.  **subsuming inference forms**: Let the premises of any inference form be
    abbreviated by $$\alpha$$ and its conclusions by $$\beta$$; then "not
    both: $$\alpha$$ and not $$\beta$$" is a propositional form which
    accurately expresses the inference form.

### The Propositional Calculus

### The Predicate Calculus

A _predicate_ is an expression that represents some property an individual can
possess. Propositions can be built up from propositions, predicates, or some
combination of the two.

For instance:

*   "Aristotle is brilliant"
    - "... is brilliant" = $$\phi$$
    - "Aristotle" = $$x$$
    - predicate = $$\phi{x}$$, a one-place predicate (_monadic_)
*   "Joe is the son of Abe"
    - "... is the son of ..." = $$\phi$$
    - "Joe" = $$x$$
    - "Abe" = $$y$$
    - predicate = $$\phi{xy}$$, a two-place predicate (_dyadic_)
*   "Joe is between a rock and a hard place"
    - "... is between ... and ..." = $$\phi$$
    - "Joe" = $$x$$
    - "a rock" = $$y$$
    - "a hard place" = $$z$$
    - predicate = $$\phi{xyz}$$, a three-place predicate

Terminology:

1.  **predicate**: An expression that represents some _property_ an individual can
    possess.
    * **property**: Either some attribute or some state of being in _relation_ to
      other things, such as spatial locality or temporal existence
2.  **predicate variable**: Any variable used to represent a predicate;
    usually a greek letter such as $$\phi$$, $$\psi$$, or $$\chi$$.
3.  **well-formed formula (wff)**: Any _predicate variable_ followed by any number
    of _individual variables_ (replaceable by names of individuals). The notion
    of well-formednes may be restricted by the _arity_ of a predicate in some
    systems.
4.  **atomic formula**: Any wff.
5.  **arity/degree**: The number of arguments, or _individual variables_ a
    predicate takes; can be fixed or variable. Fixed forms are termed _n-ary_,
    where n represents the number of arguments. For instance: 1-ary (_monadic_),
    2-ary (_dyadic_). This same notion is also denoted by _degree n_ and can
    also be denoted using a superscript: $$\phi^2{xyz}$$ (which is not a wff).

#### Truth-Functional Operators

Atomic formulas may be combined with _truth-functional operators_ to give
formulas such as $$\phi{x} \lor \psi{y}$$. For example: "Either the customer (x)
is friendly ($$\phi$$) or else John (y) is disappointed ($$\psi$$)."

Aliases:

*   Logical Connectives
*   Sentential Connectives
*   Propositional Connectives

Terminology:

1.  **connective**: A word or group of words that can be used to join two or
    more propositions together to form a _connective proposition_.
2.  **connective proposition**: A proposition which contains two or more
    propositions joined together by a _connective_.
3.  **conjunction ($$\land$$)**: "and"
4.  **disjunction ($$\lor$$)**: "or"
5.  **negation ($$\neg$$)**: "not"
6.  **condiitonal ($$\supset$$)**: "if ... then"
7.  **biconditional (iff)**: "if and only if"

#### Quantifiers

Additional atomic formulas can be created by combining existing atomic formulas
using _quantifiers_. Quantifiers can be used to express facts like "Everybody
loves somebody" and "Somebody loves everybody."

1.  **existential quantifier ($$\exists$$)**: "there exists"
    * $$(\exists{x})\phi{x}$$ = "For some $$x, x$$ is $$\phi$$."
    * assert that a predicate applies to some individual (of some collection/type)
2.  **universal quantifier ($$\forall$$)**: "for all"
    * $$(\forall{x})(\phi{x} \supset \psi{x})$$ = "Whatever is $$\phi$$ is $$\psi$$."
    * assert that a predicate applies to all individuals (of some collection/type)

#### Orders of Predicate Calculus

##### First-Order Predicate Calculus (FOPC)

Formation Rules:

1.  An expression consisting of a predicate variable of degree n followed by n individual
    variables is a wff
2.  If $$\alpha$$ is a wff, so is $$~\alpha$$
3.  If $$\alpha$$ and $$\beta$$ are wffs, so is $$(\alpha \lor \beta)$$
4.  If $$\alpha$$ is a wff and $$a$$ is an individual variable, then
    $$(\forall{a}\alpha$$ is a wff.

##### Higher-Order Predicate Calculus (HOPC)

#### Modal Logic

#### Set Theory

## Logic Programming Languages

### Prolog

### CycL

