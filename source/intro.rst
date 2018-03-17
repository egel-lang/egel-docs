Introduction
============

Egel is a small toy language based on untyped eager combinator rewriting. Or, 
equivalently, it is an untyped lambda calculus with constants and eager semantics.

It roughly falls into the same category of combinator languages like Q and conceptually
predates languages like Miranda, ML or Haskell.

The language is homoiconic and supports symbolic rewriting, 
exceptions, namespaces, and concurrency. 

Semantically, the implementation is morally equivalent to an eager term rewriter on
a directed acyclic graph.

To get a taste of the language a small example is shown below.

.. code-block:: egel 

    namespace Fibonacci (
      using System

      def fib =
        [ 0 -> 1
        | 1 -> 1
        | N -> fib (N - 2) + fib (N - 1) ]
    )

    using Fibonacci

    def main = fib 5

The interpreter is implemented in C++. Sources can be downloaded from
Github_.

.. _Github: https://github.com/egel-lang/

