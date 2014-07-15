---
title: Notes on Ontology Engineering
author: Mack Sweeney
layout: post
---

Ontology engineering involves representing abstract concepts, such as Physical Objects,
Events, Time, Location, Information, and Beliefs in some common form.  The collection of
these representations is known as an ontology. There can be very limited, domain-specific
ontologies, and there can also be ontologies which attempt to represent everything in the
world. There can also be many forms of representation, ranging from natural language (NL)
taxonomies to logical propositions based on predicate calculus.


<!--more-->


### Table of Contents<a name="table-of-contents"></a>

    1.  [Engineering Methodologies](#engineering-methodologies)
    2.  [Representations](#representations)
    3.  [Categorization of Things](#categorization-of-things)
    4.  [Physical Composition](#physical-composition)
    5.  [Objects: Things vs. Stuff](#objects-things-vs-stuff)
    6.  [Measurements](#measurements)
    7.  [Events](#events)
        1.  [Processes](#processes)
        2.  [Time Intervals](#time-intervals)
        3.  [Fluents and Objects](#fluents-and-objects)
    1.  [Mental Events and Mental Objects](#mental-events-and-mental-objects)
    2.  [Reasoning Systems](#reasoning-systems)

### Engineering Methodologies<a name="engineering-methodologies"></a>

1.  A trained team of ontologists/logicians architect the ontology and write axioms (Cyc)
2.  Categories, attributes, and values are imported from an existing DB (DBPedia)
3.  Information is gathered by parsing text documents (TextRunner)
4.  Unskilled amateurs enter commonsense knowledge (OpenMind)

_Note_: Cyc has actually used all four to some extent.

### Representations<a name="representations"></a>

While some ontologies are represented using natural language, such as biological
taxonomies, those of interest in this study are those represented using formal logic,
which can be reasoned about using machines. These ontologies usually reside in one or
more databases, which contain the propositions which form the ontology. A proposition
goes through a process called **reification** to be entered as an object in the ontology
DB. Typically this simply involves making an _assertion_ in the logic programming
language being used to interact with the ontology.

Objects can be related using predicates. Such assertions are connective propositions
using one or more logical connectives and a quantifier. Naturally enough, these are
called _relationships_, or _relations_, between objects. Similarly, we can assert that an
object has certain properties using predicates to relate it to certain other objects. For
instance, we can assert that apples are red to indicate that the _color_ property of
_apple_ is _red_.

Many knowledge representation formats also allow for constraints on relations, either via
arity constraints on predicates or through type constraints on predicate arguments. For
instance, a _unary_ predicate is constrained to accept exactly one argument, while a
_binary_ predicate is constrained to accept exactly two arguments.

Note that objects may also be called _individuals_ or _entities_.

### Categorization of Things<a name="categorization-of-things"></a>

When the amount of knowledge represented in an ontology becomes sufficiently large,
categorization becomes a critical way to compartmentalize related facts for purposes of
improving reasoning efficiency and simplifying additional knowledge entry. If we take a
set theory perspective on the task, then a category can be thought of as a set of things
(things here being used to represent any_thing_). First-order logic (FOL) offers two
means of representing such sets: predicates and objects. That is, we can say that a bird
is all objects to which a particular predicate _bird_ applies, or we can say that a bird
is any object which belongs to the set of _birds_, which is itself an object.

These categories, or sets, are often called _classes_, since they are in many ways
anologous to classes in OOP. In particular, if a class has certain properties and
relationships, _specializations_, or objects of that class will also have these same
properties and relationships -- each meets the same _interface_, just as in OO languages.
Fundamentally, classes of things exist to simplify knowledge entry via inheritance and to
provide default information for certain objects, based on the _type_ (class) of that
object.

We can also define particular class-related concepts, such as _subclass_. A subclass of a
class is a subset of that class, and a class can have multiple subclasses that form an
_exhaustive decomposition_. In other words, their union is the set of objects which makes
up the _superclass_. An exhaustive decomposition which is disjoint is also known as a
_partition_. Classes may be overlapping or _disjoint_.  Furthermore, we can also think of
the objects that make up a class (set) as _instances_ of that class.

An object can also be inferred to be a member of some category by asserting conditions
for membership. For instance, if an object is a person and attending a university, it
can be stated that the object is a student.

### Physical Composition<a name="physical-composition"></a>

If we wish to say that dog has four legs, a tail, a torso, and a head, we are decomposing
the dog into its physical parts. In order to do this, we need something like a _partOf_
predicate which can be used to assert that one object is a part of another. In this
sense, a thing which can be fully characterized by its physical parts can be
_partitioned_ into those parts, and can be thought of as a _composite object_. Given the
composition of a dog described above, the object _Dog_ could then be said to be a
_CompositeObject_. Parts are different from physical characteristics, such as color,
shape, and size.

### Objects: Things vs. Stuff<a name="objects-things-vs-stuff"></a>

When we divide a dog into its parts, as above, we can say that each part of the dog is
not itself a dog. For instance, the dog's leg is not a dog. However, say we are dividing
up a log of wood by splitting it into smaller pieces. In this case, each piece of wood
split off the log is still wood. The same methodology applied to the dog would simply
produce many parts of the dog that no longer comprise a whole dog (while also being
terrible and producing quite a mess). This is a difference of _intrinsic_ (the wood)
properties vs. _extrinsic_ (the dog) properties. For instance, the atomic composition of
wood remains the same when you split it, as do its chemical properties (to an extent);
these are intrinsic properties. Meanwhile, things like weight, shape, and size, which are
extrinsic properties, are not the same between a composite object and its parts.

The process of dividing an object into distinct parts is sometimes called
_individuation_. If dividing an object into parts yields objects which are of the same
type, that object can be said to be "stuff", or "stuff-like". If the parts are not of the
same type, the object is said to be a "thing", or "thing-like". Some languages (such as
CycL), call every object a thing and distinguish between things which are "object-like"
and "stuff-like".

_Note_: There is, of course, a point at which division of an object into ever-smaller
parts ends up breaking apart molecules, which changes the "intrinsic" properties of the
object. The "thing vs. stuff" distinction is still useful, however. This observation
simply necessitates the notion of scale.

### Measurements<a name="measurements"></a>

Certain properties of objects can be _ordered_ (**ordinal**); we call these _measures_.
Measures can be represented using predicates which take numerical values and represent
that number of units. These are sometimes called _units functions_. Knowledge
representation is often not as concerned about maintaining the precise formulas involved
in relating measurements as it is about maintaing the ordering between them.

### Events<a name="events"></a>

While _situation calculus_ was constructed to represent discrete, isolated actions and
their immediate effects. _Event calculus_ expands upon this foundation to provide
enhanced temporal semantics; in particular, event calculus is built on _point of time_,
rather than _situations_.

Terminology:

1.  **fluent**: a proposition that can change over time (truth depends on time)
    *   situation calculus usually represents fluents as predicates with a time point
        argument.
    *   event calculus reifies fluent predicates as _functions_ and applies an additional
        predicate which takes the function and a time point to determine if the function
        is true at the given time

#### Processes<a name="processes"></a>

There can be _discrete events_, as well as _processes_, or _liquid events_. Processes can
be decomposed into sub-events that are also of the same category of event, while discrete
event decompositions yield objects which are not themselves types of the composite event.
This is essentially the same distinction as things vs. stuff.

#### Time Intervals<a name="time-intervals"></a>

In order to represent fluents which can change over time, it is necessary to represent
time itself. The fundamental unit can be considered the _time interval_. Time intervals
have _duration_. Intervals of 0 duration are called _time points_, or _moments_. A _time
point_ is most easily represented using the smallest unit; this is almost always seconds,
though fractions of seconds can be used as well. In order to facilitate human
readability, functions are often introduced for representing dates (second, minute, day,
month, year), based on the fundamental unit chosen.

Time intervals allow temporal relationships between events, such as notions of
overlapping and disjoint events. We can also represent constraints such as: if one event
causes another, it must start before it. So we can say an event begins at a certain time
and ends at another time, and it is occurring at any time between its start and end
times.

#### Fluents and Objects<a name="fluents-and-objects"></a>

These notions are useful, but they must be tied back to the non-fluent objects in order
to create relations between the two. For instance, say we have a predicate _Chair_, which
takes as an argument an instance of _Department_, which is a department of a university.
The actual object that the function _Chair_ represents will change depending on the time.
In this sense, it is a single object which is actually representing a collection of
objects; _Chair(CSDepartment)_ is actually the collection of all chairs of the CS
department, and the object it will be equal to will change depending on the time. Given
some functin _atTime_, which takes a proposition and a time point and evaluate the
proposition in the context of the time point, we can then ask questions like:
_atTime(Equal(BobMiller, Chair(CSDepartment)), AD2014)_.

### Mental Events and Mental Objects<a name="mental-events-and-mental-objects"></a>

The idea that information (facts) exist in the minds of agents necessitates the idea of
inconsistent facts and incomplete references. More specifically, FOL typically maintains
the property of _referential transparency_; any terms that refer to the same object are
logically equivalent. This is not always true when there are mental objects, since the
agents may not know that two different sentences actually refer to the same object. For
instance, an agent that does not know arithmetic will not understand that _2 + 2_
refers to the same object as _4_; this agent does not know that these terms are
_co-referential_. For concepts like this, we need _modal logic_.

Modal logic allows us to express different _models_, or _possible worlds_, which are each
some set of objects and relations/interpretations. Each of these worlds is then
_accessible_ to an agent through an _accessibility relation_. Since there are an infinite
number of possible worlds, it is important to only express those which are necessary for
the reasoning tasks at hand.

With modal logic, we gain the tools necessary to express things such as "John knows rain
is in the weather prediction", while also expressing that "Sally does not know the
weather prediction for tomorrow". Furthermore, we can state that "John knows his name is
John", and "John knows that he knows that his name is John"; this last statement is an
example of representing an agent's knowledge about its own knowledge. This is useful for
questions modal questions such as "What things does John know?"

Modal logic is still limited in the sense that it assumes all agents know everything they
can logically conclude from their asserted knowledge - _logical omniscience_. This is not
necessarily true, since an agent may not have had the time to sit down and reason about
its knowledge enough to make those conclusions.

### Reasoning Systems<a name="reasoning-systems"></a>

1.  Semantic networks
2.  Description logics

#### Monotonicity and Default Logic<a name="monotonicity-and-default-logic"></a>

Monotonicity of entailment requires that any true statement continues to be true after
adding new axioms. Logics with this property are called _monotonic logics_. This is
generally ok, except when there are inheritance situations in which the child class has
more specific assertions than a parent class. For instance, a tomatoe can be red in
general, but an unripe tomotoe is green. This sort of _default logic_ cannot be expressed
in monotonic logics.

There are three main formalisms for nonmonotonic inference, all introduced in 1980:

1.  Circumscription, McCarthy
2.  Default Logic, Reiter
3.  Modal Nonmonotonic Logic (NML), McDermott & Doyle

## Sources<a name="sources"></a>

1.  Russell, S. and Norvig, P. 1995. Artificial Intelligence : A Modern Approach,
    Englewood Cliffs, NJ: Prentice-Hall.
2.  Wikipedia: Various articles
