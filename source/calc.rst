The Calculus
============

Egel is based upon a small combinator calculus with a limited number
of constructs. Below, that calculus is introduced with small
examples.

Constants
---------

The smallest Egel expression is a constant.

.. code-block:: egel

    >> 0
    0

Multiple constants compose.

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

The nameless pattern-matching abstraction
------------------------------------------

The basic work-horse of Egel is the nameless pattern-matching
combinator. Roughly similar to an untyped lambda abstraction,
where variables are uppercase.

.. code-block:: egel

    >> [ X -> X ] 5
    5

The nameless pattern-matching combinator may consist of multiple
alternatives which pattern match from left to right. You can
mix variables and constants in patterns.

.. code-block:: egel

    >> [ 0 -> "zero" | 1 -> "one" | X -> "a lot" ] 1
    "one"

You can match against multiple values.

.. code-block:: egel

    >> [ X, Y -> X - Y ] 4 1
    3

.. caution::

    Often, you will want to put a space after a `-` symbol. Can
    you guess why? It's because constants compose, so `2-1` are
    the two constants `2` and `-1`. Make sure to insert the space!

You can define combinators as named abstractions for terms.

.. code-block:: egel

    >> def id = [ X -> X ]
    >> id "Hi!"
    "Hi!"

Definitions may mention themselves, then they are recursive.

.. code-block:: egel

    >> def fac = [ 1 -> 1 | N -> N * fac (N - 1) ]
    >> fac 3
    6

.. note::

    If you don't understand the above definition then try replacing
    `fac` in the term `fac 3`. Like this, `fac 3 = 3 * fac (3 - 1) 
    = 3 * fac 2 = 3 * 2 * fac 1 = 3 * 2 * 1 = 6`. Otherwise,
    look up 'recursion' on the Internet. Good luck!

Egel refuses to rewrite, or reduce, definitions where none of the
patterns matched.

.. code-block:: egel

    >> def z = [ 0 -> 0 ]
    >> z 1
    (z 1)

In the example above, the combinator `z` can only reduce a `0`,
when given a `1` as an argument the interpreter refuses to reduce
the term.

Helpful shorthands
------------------

With `let/in` you can bind a variable to a value.

.. code-block:: egel

    >> let X = 3 in X + 2
    5

A condition consists of an `if/then/else` statement.

.. code-block:: egel

    >> if 3 < 5 then "smaller" else "larger"
    "smaller"

Exceptions and exception handling
---------------------------------

Egel supports exceptions, you can `throw` any value anywhere.

.. code-block:: egel

    >> 1 + throw "don't go here"
    exception("don't go here")

You can also catch exceptions in a `try/catch` block. It reduces
the try part, any exception thrown in there will handled by
the provided catch handler.

.. code-block:: egel

    >> try 1 + throw "don't go here" catch [ E -> "caught:" E ]
    ("caught:" "don't go here")

That's the whole calculus, you can now program in Egel. 

.. _Github: https://github.com/egel-lang/


