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

An Egel script is a text file which defines one `main`
function. You don't have to do that, but then it won't
run anything.

Run the example with the Egel interpreter.

.. code-block:: bash

    user$ egel hello.eg
    Hello world!


