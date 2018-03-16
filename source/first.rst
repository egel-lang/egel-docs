Your First Programs
===================

Let's move on and define some programs. An Egel program
is a collection of scripts driven by a `main` function.

Hello World
-----------

The cannonical example to start with a new language is
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
start of with a function you should know, Fibbonaci.

.. code-block:: egel

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
space.

.. code-block:: egel
    namespace Fibbonaci (

        def fib =
            [ 0 -> 1
            | 1 -> 1
            | N -> fib (N - 1) + fib (N - 2) ]

    )

    def main = Fibbonaci.fib 5


