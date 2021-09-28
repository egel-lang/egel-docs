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
function.

You can run the example with the Egel interpreter.

.. code-block:: bash

    user$ egel hello.eg
    Hello world!

Interactive Mode
----------------

Apart from batch mode, you can also run the intpreter
interactively.

The interpreter starts with a clean slate, you'll usually
want to start of with a `using System` directive to access 
the built-in combinators.

.. code-block:: bash

    user$ egel
    > using System
    > def fac = [ 0 -> 1 | N * fac (N - 1) ]
    > fac 5
    120

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

Multiple scripts
----------------

Of course, you'll want to use and define small data
structures. That's easy in Egel, small constants can
function as constructors, although when you become more 
advanced you will often just leave them away.

While we're at it, let's pretend this is serious business 
and split our new application into two files.

Put the following code in the file `eval.eg`.

.. code-block:: egel

    namespace Eval (

        using System

        data sum, mul

        def eval =
            [ sum X Y -> eval X + eval Y
            | mul X Y -> eval X * eval Y
            | X -> X ]

    )

And write the following text to `main.eg`.

.. code-block:: egel

    import "eval.eg"

    using Eval

    def main = eval (sum 3 (mul 2 7))

The `import` directive tells the interpreter where to look.
Running `egel main.eg` should give `17`.

Values
------

Values are combinator definitions where the body is reduced
then assigned. This serves a two-fold purpose.

For one, often you'll want to compute a value once and then
reuse it without passing it around explicitly. Secondly,
due to technical reasons all definitions are wrapped in
lambda abstractions you sometimes want to get rid off.

.. code-block:: egel

     val x = heavy_computation somenumber
     
     def main = (x, x)
