Introduction
============

Egel is based on untyped eager combinator rewriting. Or, stated
differently, Egel is an untyped lambda calculus with constants
and strict semantics.

Below, a high-speed introduction to the Egel language is given
with examples.

The calculus
------------

The smallest Egel expression is a constant.

.. code-block:: egel
    >> 0
    0

Multiple constants also form a term.

.. code-block:: egel
    >> 1 2 3
    (1 2 3)

Egel supports integers, floats, characters and Unicode strings.

.. code-block:: egel
    >> 'a' 3.14 "Hello!"
    ('a' 3.14 "Hello!")

You can define your own constant combinators. Constants are lower-case.

.. code-block:: egel
    >> data one, two, three
    >> two
    two

The basic work-horse of Egel is the anonymous pattern-matching
combinator. Roughly similar to an untyped lambda abstraction,
where variables are uppercase.

.. code-block:: egel
    >> [ X -> X ] "id"
    "id"

The anonymous pattern-matching combinator may consist of multiple
alternatives which pattern match from left to right.

.. code-block:: egel
    >> [ 0 -> "zero | 1 -> "one" ] 1
    "one"

You can define combinators as named abstractions for terms.

.. code-block:: egel
    >> def id = [ X -> X ]
    >> id "Hi!"
    "Hi1"

Definitions may be recursive.

.. code-block:: egel
    >> def fac = [ 1 -> 1 | N -> N * fac (N - 1) ]
    >> fac 3
    6

Egel refuses to rewrite, or reduce, definitions where none of the
patterns matched.

.. code-block:: egel
    >> def z = [ 0 -> 0 ]
    >> z 1
    (z 1)

In the example above, the combinator `z` can only reduce a `0`,
when given a `1` as an argument the interpreter refuses to reduce
the term.

With `let` you can bind a variable to a value.

.. code-block:: egel
    >> let X = 3 in X + 2
    5

A condition consists of an if/then/else statement.

.. code-block:: egel
    >> if 3 < 5 then "smaller" else "larger"
    "smaller"

Egel supports exceptions. You can throw any value anywhere.

.. code-block:: egel
    >> 1 + throw "don't go here"
    exception("don't go here")

You can also catch exceptions in a try/catch block.

.. code-block:: egel
    >> try 1 + throw "don't go here" catch [ E -> "caught:" E ]
    ("caught:" "don't go here")

That's the whole calculus, you can now program in Egel. 
Now let's continue with some interesting things!


.. _Github: https://github.com/egel-lang/

