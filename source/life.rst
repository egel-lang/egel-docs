Conway's Game of Life
=====================

To showcase that Egel can be used to write real
programs I'll walk you through an example of 
a small Conway's life application. I'll assume you
know some functional programming, some territory not
covered yet comes along too.

Conway's game of life plays on a grid. At any point
a cell on the grid may be dead or alive. Any life
cell with fewer than two, or more than three,
neighbours dies. Any dead cell with exactly three
neighbours comes alive.

Preamble
--------

It's good practice to start every file with some
comment on what it implements.

.. code-block:: egel

    /**
     * Conway's Game of Life.
     */

Like a lot of languages, comments spanning multiple
lines start with `/*` and end with `*/`. Single-line
comments start with `//`.

We'll rely on combinators defined in `prelude.eg` and
`io.ego`. A `.ego` file is an object file, a binary
on your system.

.. code-block:: egel

    import "prelude.eg"
    import "io.ego"

We'll open up the different namespaces we need from
those files.

.. code-block:: egel

    using System
    using List
    using IO

The board
---------

The board size of the two-dimensional grid is defined
with a constant.

.. code-block:: egel

    def boardsize = 5

So, now the real programming starts. The grid is implemented
as a stencil. A stencil is a function mapping coordinates to
cells. A cell `0` is dead, any other value means it's alive.

The empty grid maps all coordinates to dead cells.

.. code-block:: egel

    def empty = [ X Y -> 0 ]

To insert an alive cell, we update the stencil with a clause
mapping two matching coordinates to an alive cell.

.. code-block:: egel

    def insert =
        [ X Y BOARD -> 
            [ X0 Y0 -> if and (X0 == X) (Y0 == Y) then 1
                        else BOARD X0 Y0 ] ]

To get to all coordinates we map multiple times on the list
`{0,..,boardsize-1}` to retrieve the pairs `{{0 0, 0 1, ..},..}`.
Note that we don't need to tuple explicitly.

.. code-block:: egel

    def coords =
        let R = fromto 0 (boardsize - 1) in
            [ XX YY -> map (\X -> map (\Y -> X Y) YY) XX ] R R

Printing
--------

To print, we just apply `IO.print` for a dead or alive cell.
Though Egel is a mostly pure term rewrite system, combinators loaded may
have side effects.

.. code-block:: egel

    def printcell =
        [ 0 -> print ". "
        | _ -> print "* " ]

A wildcard pattern `_` is used to match against any value.

Printing a board is done by going over all coordinates and printing the
cell for that coordinate.

.. code-block:: egel

    def printboard =
        [ BOARD ->
            foldl [_ XX -> map [(X Y) -> printcell (BOARD X Y)] XX; print "\n" ] nop coords ]

.. note:: 

    Though Egel combinators may be side-effecting, they must reduce to a value.
    `IO.print` will print all its arguments but will reduce to the uninformative
    value `System.nop`. Often, with side-effecting calculations these values
    are simply discarded. The semicolon separates such statements.

Generations
-----------

The neighbour count of a coordinate on a board can be calculated by just
looking around.

.. code-block:: egel

    def count =
        [ BOARD X Y ->
            (BOARD (X - 1) (Y - 1)) + (BOARD (X) (Y - 1)) + (BOARD (X+1) (Y - 1)) +
            (BOARD (X - 1) Y) + (BOARD (X+1) Y) +
            (BOARD (X - 1) (Y+1)) + (BOARD (X) (Y+1)) + (BOARD (X+1) (Y+1)) ]

The status of the next cell is calculated from whether the current cell
is alive or dead and the number of neighbours.

.. code-block:: egel

    def next =
        [ 0 N -> if N == 3 then 1 else 0
        | _ N -> if or (N == 2) (N == 3) then 1 else 0 ]

A board is updated by applying the above function `next` to every coordinate
on the board.

.. code-block:: egel

    def updateboard =
        [ BOARD ->
            let XX = map (\(X Y) -> X Y (BOARD X Y) (count BOARD X Y)) (flatten coords) in
            let YY = map (\(X Y C N) -> X Y (next C N)) XX in
                foldr [(X Y 0) BOARD -> BOARD | (X Y _) BOARD -> insert X Y BOARD ] empty YY ]

A blinker
---------

A blinker consists of three alive cells next to each other.

.. code-block:: egel

    def blinker =
        (insert 1 2) @ (insert 2 2) @ (insert 3 2)

We print three generations of a board with a blinker.

.. code-block:: egel

    def main = 
        let GEN0 = blinker empty in
        let GEN1 = updateboard GEN0 in
        let GEN2 = updateboard GEN1 in
            foldl [_ G -> print "generation:\n"; printboard G ] nop {GEN0, GEN1, GEN2}

And that wraps it up. A real Egel application.

