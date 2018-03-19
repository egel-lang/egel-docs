Installation
============

The Egel interpreter is a small C++ application and is for the
moment not distributed in binary form. You will need to download
and compile it yourself.

Building from sources
---------------------

The interpreter is developed on a Linux system and uses libicu for
Unicode support. You need to have GCC/g++, the GNU compiler chain,
and the development files for libicu
installed. Most Linux package managers will provide that for you.

The sources can be obtained from Github_.

To compile the system run the `build.sh` script.
That should give you an interpreter named `egel` in the `src` directory
and a number of dynamically loadable Egel object files in the
`include` directory.

Installing the interpreter
--------------------------
To install the system run the `install.sh` script as root. On a Fedora
system..

If you don't want a system-wide install, please note that you only need the 
interpreter named `egel` and all files in the `include` directory 
if you want to do anything useful.
You can set the environment variable `EGEL_INCLUDE` to point
at the latter path.

Using the interpreter
---------------------

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

.. _Github: https://github.com/egel-lang/


