Concurrency
===========

Because Egel is a term rewrite language, it is trivial
to rewrite terms in parallel. Concurrency is provided
through a combinator.

Parallel rewriting
------------------

If you want to have two computations run in parallel
use the `par` combinator. It takes two abstractions
to be reduced, applies both of them to a dummy argument,
and returns a tuple containing both results.

.. code-block:: egel

    >> using System
    >> par [ _ -> 1 + 2 ] [ _ -> 3 + 4 ]
    (System:tuple 3 7)

.. note::
    The `par` combinator takes two abstractions because 
    Egel has strict semantics. If it would have been
    just `par (1+2) (3+4)` the interpreter would have
    reduced the arguments to `par` first, resulting
    in the parallel reduction of `par 3 7`. By wrapping
    the computations their evalution is deferred.

We can inspect what arguments are given to the abstractions
of `par`.

.. code-block:: egel

    >> using System
    >> par [ X -> X ] [ X -> X ]
    (System:tuple System:nop System:nop)

Hardly interesting.

Of course, you might want to supply arguments to both
terms to be reduced. Then simply wrap them in an abstraction
again.

.. code-block:: egel

    >> using System
    >> [ X -> par [ _ -> X * 3 ] [ _ -> X + 5 ] ] 4
    (System:tuple 12 9)

Parallel Fibonacci
------------------

With all what we know now, we can implement parallel
Fibonacci.

.. code-block:: egel

    import "prelude.eg"

    namespace Fibonnaci (
      using System

      def pfib = 
        [ 0 -> 0 
        | 1 -> 1 
        | X -> [ (F0, F1) -> F0 + F1 ] (par [_ -> pfib (X - 1) ] [_-> pfib (X - 2)]) ]

    )

    using Fibonnaci
    using System

    def main = pfib 10

In the recursive alternative of `pfib` it will start up two
parallel computations, reduce those, after which it will
deconstruct the pair returned and add both components.

Nifty, huh?

.. caution:: 

    Though morally Egel could support cheap concurrency, the
    `par` combinator is implemented with the C++ thread library,
    thus with system threads.

    System threads are a bit heavyweight and easy to run out
    of. On my machine, I can start upto roughly 20,000 threads.
    Go easy on `pfib`!
