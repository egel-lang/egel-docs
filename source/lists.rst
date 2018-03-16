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
from the `System` namespaces. Of course, you are
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
    System.cons 'a' (System.cons 1 System.nil)

