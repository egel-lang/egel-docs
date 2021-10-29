Discussion
==========

Egel is a untyped functional scripting language based on an eager 
combinator calculus implemented as a term rewriting system on a directed 
acyclic graph (DAG) through lifting C++.

What does that mean? You can easily conclude a number of things
from that although you can discuss those conclusions endlessly.

1. Egel is untyped. That means you get an immense amount of
   expressive power but also that
   it doesn't scale very well, though
   Lisp, Javascript, and Python practitioners might disagree with
   that. Types are great, however, for short programs they don't
   matter much, with types you just pay a little for static guarantees.

2. Terms are rewritten. Well, that's likely not a fast language
   and although the interpreter gives reasonable performance it indeed
   isn't fast. Though, through Herculean effort, term rewrite systems
   can be made performant, I don't have that much time. However,
   the interpreter gives you a pretty robust system and that's
   worth something too.

3. It rewrites a DAG. With mutation you'll be the one to make
   sure that your run-time structures don't contain cycles.

4. C++. That's another tradeoff. C++ objects are heavyweight
   so you pay again in performance but you get a bit more reliable
   system back. The good part is that it is relatively easy
   to safely drop C++ functionality into combinators.

In conclusion, Egel is a solution for people who need a 
small declarative easily extendable language which effortlessly binds
to C/C++ and who don't expect to write very large or imperative programs.
It tries to support a niche market.

Apart from that, you can have great fun writing Egel programs
so don't let any of the above stop you!

