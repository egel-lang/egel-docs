Installation
============

The Egel interpreter is a small C++ application and is for the
moment not distributed in binary form. You will need to download
and compile it yourself.

Building from sources
---------------------

The interpreter is developed on MacOS/Linux system. 
You need to have the compiler chains for gcc or llvm, cmake,
and the development files for icu and fmt
installed. Most Linux/Macos package managers will provide that for you.

The sources can be obtained from Github_.

Compilation follows the default cmake scheme, read the README
text in the distribution.

Using the interpreter
---------------------

The interpreter supports various modes: batch processing, REPL
(read-eval-print-loop), and direct commands.

A number of example scripts are provided in the examples directory.
If you set up your system correctly, you can run any of them
with the command `egel example.eg`.

.. code-block:: bash

    user$ egel examples/fib.eg
    10946

.. tip::

    The interpreter has a REPL, an interactive mode, but doesn't 
    support line editing or completion. I use the console
    program `rlwrap` for that. It should be installed or be
    provided by your distribution. To use the interpreter
    in interactive mode with line editing run the command
    `rlwrap egel`.

At the prompt of the Egel interpreter you can type small
expressions.

.. code-block:: egel

    user$ egel
    >> 1 + 2
    3

However, you'll likely want more functionality. It is recommended
you always import the prelude and open the necessary namespaces.

.. code-block:: egel

    >> import "prelude.eg"
    >> using System
    >> using List
    >> foldl (+) 0 {1,2,3}
    6
    
Lastly, you can provide commands directly to the interpreter and
use it as a simple command-line calculator.

.. code-block:: bash

    user$ egel fib.eg -e "using Fibonnaci;; fib 5"
    5

.. _Github: https://github.com/egel-lang/


