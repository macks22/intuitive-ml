---
title: Formal Logic: Foundations of Knowledge Representation and Reasoning (KRR)
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


## Table of Contents

1.  [History](#history)
2.  [The Predicate Calculus](#the-predicate-calculus)
    1.  [Formal Logic](#formal-logic)
        1.  [A Deductive Argument](#a-deductive-argument)
        2.  [Deductive Inference](#deductive-inference)
    2.  [The Propositional Calculus (PC)](#the-propositional-calculus-(pc))
        1.  [Propositional Connectives (Operators)](#propositional-connectives-(operators))
        2.  [Formation Rules of PC](#formation-rules-of-pc)
        3.  [Valid Formulas and Deductive Rules of PC](#valid-formulas-and-deductive-rules-of-pc)
        4.  [Axiomatization of PC](#axiomatization-of-pc)
            1.  [Principia Mathematica (PM)](#principia-mathematica-(pm))
    3.  [The Predicate Calculus](#the-predicate-calculus)
        1.  [Quantifiers](#quantifiers)
        2.  [Truth-Functional Operators](#truth-functional-operators)
        3.  [Conditions of Truth and Falsity](#conditions-of-truth-and-falsity)
        4.  [Orders of Predicate Calculus](#orders-of-predicate-calculus)
            1.  [First-Order Predicate Calculus (FOPC)](#first-order-predicate-calculus-(fopc))
        1.  [Modal Logic](#modal-logic)

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
    * the _premises_ are often stated as "given" in a logical proof.
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
    accurately expresses the inference form. In this way, the class of
    propositional forms subsume the class of inference forms.

### The Propositional Calculus (PC)

The simplest and most basic branch of logic. It deals only with complete,
unanalyzed propositions and certain combinations into which they can enter.
In other words, it deals with _formulas_ rather than _sentences_.

1.  **variables**: Represent unspecified propositions - mark the places in
    formulas into which sentences (and only sentences) may be inserted
2.  **truth value**: Every proposition is either true or false.
3.  **well-formed formula (wff)**: any proposition which is formed from an
    acceptable sequence of symbols, as specified by the _formation rules of
    PC_.
4.  **sentence**: Any wff with no free variables.
    *   take a wff and uniformly substitue values for its variables and you
        get a sentence, which may be either true or false

#### Propositional Connectives (Operators)

_Connective propositions_ can be built up by connecting other propositions
using one or more _connectives_.

1.  **connective**: A word or group of words that can be used to join two or
    more propositions together to form a _connective proposition_.
2.  **connective proposition**: A proposition which contains two or more
    propositions joined together by a _connective_.
3.  **conjunction ($$\land$$)**: "and"
    *   $$p \land q$$ is true when p and q are both true and false in all other cases
    *   note that the "$$\bullet$$" symbol was previously used for conjunction
4.  **disjunction ($$\lor$$)**: "or"
    *   $$p \lor q$$ is false when p and q are false and true in all other cases
5.  **negation ($$\neg$$)**: "not"
    *   $$\neg$$p is false when p is true and true when p is false
    *   note that the "~" symbol is often used interchangeably with $$\neg$$
6.  **conditional ($$\longrightarrow$$)**: "if ... then"
    *   $$p \longrightarrow q$$ is true only when p is true and q is true
    *   means "if p is true, then q is also true"
    *   first argument known as _antecedent_, second as _consequent_
    *   note that the $$\supset$$ symbol is often used for conditional in older
        texts, but it is easy to confuse with the idea of "superset" from set theory
7.  **material implication ($$\implies$$)**:
    *   "$$P \implies Q$$" means $$P \longrightarrow Q$$ is a tautology
    *   in other words, $$Q$$ is true whenever $$P$$ is true
8.  **biconditional ($$\longleftrightarrow$$)**: "if and only if" aka "both or neither"
    *   $$p \longleftrightarrow b$$ is logically equivalent to
        $$(p \longrightarrow q) \land (q \longrightarrow p)$$
    *   also logically equivalent to XNOR (exclusive nor) boolean operator
9.  **material equivalence ($$\iff$$)**:
    *   "$$P \iff Q$$" means $$P \longleftrightarrow Q$$ is a tautology
    *   can be thought of as an equals sign for propositions
10. **logical equivalence ($$\equiv$$)**: "is equivalent to"
    *   $$P \equiv Q$$ means Q has the same logical content (truth table) as P
11. **syntactic consequence ($$\vdash$$)**: "provable"
    *   "$$A \vdash B$$" means $$A$$ is provable from $$B$$
    *   may also see "$$A \vdash_{FS} B$$", which is the same thing
        +   $$FS$$ here means _formal system_
12. **semantic consequence ($$\models$$)**: "entails"
    *   "$$A \models B$$" is true if and only if there is no model $$M$$ in which all
        members of $$A$$ are true and $$B$$ is false
    *   In other words, the set of interpretations that make all members of $$B$$ true is
        a subset of the interpretations that make $$A$$ true

#### Formation Rules of PC

Formation rules specify which sequences of symbols count as acceptable, aka
well-formed formulas (wff).

1.  A variable standing alone is a wff
2.  If $$\alpha$$ is a wff, so is $$\neg{\alpha}$$
3.  If $$\alpha$$ and $$\beta$$ are wffs, so are the following:
    *   ($$\alpha \land \beta$$)
    *   ($$\alpha \beta$$)
    *   ($$\alpha \lor \beta$$)
    *   ($$\alpha \longrightarrow \beta$$)
    *   ($$\alpha \longleftrightarrow \beta$$)

These rules are often relaxed slightly to allow exclusion of brackets/parentheses
where they are not necessary to disambiguate propositions.

*   $$p \land q \land r$$ instead of $$p \land (q \land r)$$
*   $$p \land (q \longrightarrow r) \land \neg{r}$$ instead of $$[p \land (q
    \longrightarrow r)] \land \neg{r}$$

#### Valid Formulas and Deductive Rules of PC

See [relevant Wikipedia
section](http://en.wikipedia.org/wiki/Propositional_calculus#Basic_and_derived_argument_forms)

#### Axiomatization of PC

A particular _axiomatic system_ is specified by its _axiomatic basis_. A certain
set of wffs are chosen to _axioms_, _transformation rules_ are specified for
deriving further wffs, known as _theorems_ from the _axioms_.

1.  **axiomatic basis**: consists of 4 things:
    1.  list of primitive symbols, together with any convenient _definitions_
    2.  set of formation rules, specifying which symbols count as wffs
    3.  list of wffs selected as axioms
    4.  a set of one or more transformation rules for deriving theorems
2.  **axiom**: A wff chosen to represent ground truth for a particular axiomatic basis
3.  **theorem**: A wff derived from an axiom and the set of _transformation rules_
4.  **transformation rule**: A rule for deriving theorems from axioms, which
    involves the repositioning of certain symbols in a wff given certain symbols.
5.  **definitions**: Can function as additional transformation rules
    *   any expression of the form occuring on one side is replaced by the corresponding
        expression of the form occuring on the other side
    *   the result of using a definition as a tranformation rule is a theorem
6.  **sound**: An axiomatic system is sound if every theorem is valid
7.  **complete**: An axiomatic system is complete if every valid wff is a theorem

**Principia Mathematica (PM)**<a name="principia-mathematica-(pm)"></a>

The text in which Bertrand Russell and Alfred North Whitehead derived what is
possibly the best-known axiomatic system for PC; also often used as the name
of that same system.

Axiomatic basis:

*   **primitive symbols**: ~, $$\lor$$, (,), and an infinite set of variables,
    $$p, q, r, ...$$ (with or without subscripts)
*   **definitions**: $$\bullet$$, $$\supset$$, $$\equiv$$ (equivalence)
*   **formation rules**: see _formation rules of PC_
*   **axioms**:
    1.  $$(p \lor p) \supset p)$$
    2.  $$q \supset (p \lor q)$$
    3.  $$(p \lor q) \supset (q \lor p)$$
    4.  $$(q \supset r) \supset [(p \lor q) \supset (p \lor r)]$$
*   **transformation rules**:
    1.  The result of uniformly replacing any variable in a theorem by any wff is a
        theorem (rule of substitution).
    2.  If $$\alpha$$ and ($$\alpha \supset \beta$$) are theorems, then $$\beta$$ is
        a theorem (rule of detachment, aka modus ponens)

### The Predicate Calculus

A _predicate_ is an expression that represents some property an individual can
possess. Propositions can be built up from propositions, predicates, or some
combination of the two. Predicate logic is also called **Logic of Quantifiers**.

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

#### Quantifiers

Additional atomic formulas can be created by combining existing atomic formulas
using _quantifiers_. Quantifiers can be used to express facts like "Everybody
loves somebody" and "Somebody loves everybody."

1.  **existential quantifier ($$\exists$$)**: "there exists"
    * $$(\exists{x})\phi{x}$$ = "For some $$x, x$$ is $$\phi$$."
    * assert that a predicate applies to some individual (of some collection/type)
2.  **universal quantifier ($$\forall$$)**: "for all"
    * $$(\forall{x})(\phi{x} \longrightarrow \psi{x})$$ = "Whatever is $$\phi$$ is $$\psi$$."
    * assert that a predicate applies to all individuals (of some collection/type)

#### Truth-Functional Operators

Atomic formulas may be combined with _truth-functional operators_ to give
formulas such as $$\phi{x} \lor \psi{y}$$. For example: "Either the customer (x)
is friendly ($$\phi$$) or else John (y) is disappointed ($$\psi$$)."

Aliases:

*   Logical Connectives
*   Sentential Connectives
*   Propositional Connectives

#### Conditions of Truth and Falsity

There are three mutually exclusive classes of atomic formulas (aka predicate sentences)
that exist:

1.  **tautology**: true on every possible specification of predicate signs
    *   "Everything is F or is not F"
2.  **inconsistent**: false on every possible specification of predicate signs
    *   "Something is F and not F"
3.  **contingent**: true on some specifications and false on others
    *   "Something is F and is G"

#### Orders of Predicate Calculus

First-order predicate calculus (FOPC) is constrained so that only individual
variables can occur in quantifiers. Second-order predicate calculus (SOPC)
also allows predicate variables to occur in quantifiers.

##### First-Order Predicate Calculus (FOPC)

Formation Rules:

1.  An expression consisting of a predicate variable of degree n followed by n
    individual variables is a wff.
2.  If $$\alpha$$ is a wff, so is $$~\alpha$$
3.  If $$\alpha$$ and $$\beta$$ are wffs, so is $$(\alpha \lor \beta)$$
4.  If $$\alpha$$ is a wff and $$a$$ is an individual variable, then
    $$(\forall{a}\alpha$$ is a wff.

#### Modal Logic

[Coming eventually...]

## Sources

1.  [Encyclopedia Britannica: Formal
Logic](http://www.britannica.com/EBchecked/topic/213716/formal-logic/65842/The-predicate-calculus?anchor=ref534682)
2.  [Various subsections of Wikipedia: Logic](http://en.wikipedia.org/wiki/Logic)
