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

An installation script is not provided since Linux systems tend
to have divergent opinions on where to place different parts of
a tool.

Instead, please note that you only need the interpreter named
`egel` and all files in the `include` directory if you want to
do anything useful.
You can set the environment variable `EGEL_INCLUDE` to point
at the latter path.

A number of example scripts are provided in the examples directory.
If you set up your system correctly, you can run any of them
with the command `egel example.eg`.

.. _Github: https://github.com/egel-lang/


