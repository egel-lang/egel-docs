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
    System:nil

Creating a list is trivial.

.. code-block:: egel

    >> cons 'a' (cons 1 nil)
    {'a', 1}

Curly braces are syntactic sugar for lists.

Let's proceed with defining functions on lists.
A length function is the first we'll try.

.. code-block:: egel

    >> def length = [ nil -> 0 | cons X XX -> 1 + length XX ]
    >> length {'a', 1}
    2

Egel is untyped, you might make a typo and apply
`length` to something not a list. Can you guess what will
happen?

.. code-block:: egel

    >> length 0
    (length 0)

The patterns are exhausted therefor the term will fail to
reduce.

Functional programmers adore lists, there's a lot one
can do with them, if not everything. Egel suplies a number
of convenience routines in the `List` namespace in the 
`prelude`.

.. code-block:: egel

    >> import "prelude.eg"
    >> using List

I'll assume that you know some functional programming.
Standardly, we can apply any
function `f` to any list with the `map` combinator.

.. code-block:: egel

    >> map [X -> X + 1] {0,1}
    {1, 2}

This documentation is on the Egel language, it's not
an introduction to functional programming. But did
you get what happened there? `map` applied `[X->X+1]`
to both elements of the list `{0,1}` resulting in
the list `{1,2}`.
    
And the important `foldl` is defined too. It's a useful
operator but don't go overboard with it!

.. code-block:: egel

    >> foldl (+) 0 {1,2,3}
    6
    
`foldl` will fold a function and a constant over a list,
`foldl (+) 0 {1,2,3} = 1 + (2 + (3 + 0))`. It's a summation.

Tuples
------

Tuples in languages are used to group things. It's a useful
feature which you don't always need in Egel since constants
compose. Let's find out how they work.

Like lists, tuples are syntactic sugar for applying the
`tuple` constant out of the `System` namespace to a number
of arguments.

.. code-block:: egel

    >> (1,"hi")
    (System:tuple 1 "hi")

Again, it's all untyped so we can try to match against
a tuple to find out how many fields it has.

.. code-block:: egel

    >> def c = [ (X,Y) -> 2 | (X,Y,Z) -> 3 ]
    >> c ("what", "a", "night")
    3

That's all for that subject. If you start programming Egel
you'll find many more useful constructs.

.. note::

    Egel has a concise syntax, so you might easily get confused 
    between alternatives.

    The folowing reduces two arguments. Two patterns, each one variable.

    .. code-block:: egel

        >> [X Y -> X] 0 1
        0

    And this rewrites two composed constants. One pattern of two variables.

    .. code-block:: egel

        >> [(X Y) -> X] (0 1)
        0

    And finally, this rewrites a tuple. One pattern using sugar for a tuple.

    .. code-block:: egel

        >> [(X, Y) -> X] (0, 1)
        0
