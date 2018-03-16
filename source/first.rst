Your First Programs
===================

Let's move on and define some programs. An Egel program
is a collection of scripts driven by a `main` function.

Hello World
-----------

We'll start with the cannonical example for a new language 
"hello world". Edit the file `hello.eg` and add the
following content.

.. code-block:: egel

    def main = "Hello world!"

An Egel script is a text file which may define one `main`
function. You don't have to do that, but then it won't
run anything.

Run the example with the Egel interpreter.

.. code-block:: bash

    user$ egel hello.eg
    Hello world!

More functions
--------------

More functions make for more interesting scripts. Let's
start of with a function you should know, faculty.

The interpreter starts with a clean slate, you'll need
to give a `using System` directive to access the builtin
math combinators.

.. code-block:: egel

    using System

    def fib =
        [ 0 -> 1
        | 1 -> 1
        | N -> fib (N - 1) + fib (N - 2) ]

    def main = fib 5

Save it somewhere, run it, and it should give you a number.

Adding namespaces
-----------------

Functions live in namespaces. A namespace starts with
a capital letter and names all combinators within the
space. Let's move on to the venerable Fibonacci.

.. code-block:: egel

    namespace Fibonacci (

        using System

        def fib =
            [ 0 -> 1
            | 1 -> 1
            | N -> fib (N - 1) + fib (N - 2) ]

    )

    using Fibonacci

    def main = fib 5

A small evaluator
-----------------

Of course, you'll want to use and define small data
structures. That's easy in Egel, small constants can
function as constructors, although when you become more 
advanced you will often just leave them away.

.. code-block:: egel

    namespace Eval (

        using System

        data sum, mul

        def eval =
            [ sum X Y -> X + Y
            | mul X Y -> X * Y
            | X -> X ]

    )

    using Eval

    def main = eval (sum 3 (mul 2 7))


