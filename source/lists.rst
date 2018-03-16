Lists and Tuples
================

Right, so you've seen constants, abstractions, and a 
means to split programs over files. Any pedantic
scientist can now tell you that's enough to encode
any program. Maybe that's correct, maybe not.

Let's find out.

Lists
-----

Working with lists follows a convention in Egel. They
are constructed with the `nil` and `cons` constants
from the `System` namespace. Of course, you are
free to choose any convention you like, but for now,
we kind-of rely on that programmers will follow
that convention.

You can test that the constants are there in interactive
mode.

.. code-block:: egel

    >> using System
    >> nil
    System.nil

Creating a list is trivial.

.. code-block:: egel

    >> cons 'a' (cons 1 nil)
    (System.cons 'a' (System.cons 1 System.nil))

But that's a lot of typing. Egel provides what is
called syntactic sugar for lists, a shorthand
notion employing curly brackets.

.. code-block:: egel

    >> {'a', 1}
    (System.cons 'a' (System.cons 1 System.nil))

Of course, you'ld like to define functions on these.
A length function is the first we'll try.

.. code-block:: egel

    >> def length = [ nil -> 0 | cons X XX -> 1 + length XX ]
    >> length {'a', 1}
    2

Egel is untyped, you'ld might make a type and apply
`length` to something not a list. Can you guess what will
happen?

.. code-block:: egel

    >> length 0
    (length 0)

The patterns are exhausted therefor the term will fail to
reduce.



