Download Link: https://assignmentchef.com/product/solved-cmpsc-442-homework-2
<br>
<h1>Instructions</h1>

In this assignment, you will explore three classic puzzles from the perspective of uninformed search.

A skeleton file homework2-cmpsc442.py containing empty definitions for each question has been provided. Since portions of this assignment will be graded automatically, none of the names or function signatures in this file should be modified. However, you are free to introduce additional variables or functions if needed.

You may import definitions from any standard Python library, and are encouraged to do so in cases where you find yourself reinventing the wheel. If you are unsure where to start, consider taking a look at the data structures and functions defined in the collections, itertools, math, and

random modules.

You will find that in addition to a problem specification, most programming questions also include a pair of examples from the Python interpreter. These are meant to illustrate typical use cases to clarify the assignment, and are not comprehensive test suites. In addition to performing your own testing, you are strongly encouraged to verify that your code gives the expected output for these examples before submitting.

You are strongly encouraged to follow the Python style guidelines set forth in <a href="https://legacy.python.org/dev/peps/pep-0008/">PEP 8</a>, which was written in part by the creator of Python. However, your code will not be graded for style.

<h1>1.   N-Queens [25 points]</h1>

In this section, you will develop a solver for the <em>n</em>-queens problem, wherein <em>n</em> queens are to be placed on an <em>n x n</em> chessboard so that no pair of queens can attack each other. Recall that in chess, a queen can attack any piece that lies in the same row, column, or diagonal as itself.

A brief treatment of this problem for the case where <em>n = 8</em> is given in Section 3.2 of the textbook, which you may wish to consult for additional information.

<ol>

 <li><strong>[5 points] </strong>Rather than performing a search over all possible placements of queens on the board, it is sufficient to consider only those configurations for which each row contains exactly one queen. Without taking any of the chess-specific constraints between queens into account, implement the pair of functions num_placements_all(n) and</li>

</ol>

num_placements_one_per_row(n) that return the number of possible placements of <em>n</em> queens

on an <em>n x n</em> board without or with this additional restriction. Think carefully about why this restriction is valid, and note the extent to which it reduces the size of the search space. You should assume that all queens are indistinguishable for the purposes of your calculations.

<ol start="2">

 <li><strong>[5 points] </strong>With the answer to the previous question in mind, a sensible representation for a board configuration is a list of numbers between <em>0</em> and <em>n – 1</em>, where the <em>i</em>th number designates the column of the queen in row <em>i</em> for <em>0</em> ≤ i &lt; <em>n</em>. A complete configuration is then specified by a list containing <em>n</em> numbers, and a partial configuration is specified by a list containing fewer than <em>n</em> Write a function n_queens_valid(board) that accepts such a list and returns True if no queen can attack another, or False otherwise. Note that the board size need not be included as an additional argument to decide whether a particular list is valid.</li>

 <li><strong>[15 points] </strong>Write a function n_queens_solutions(n) that yields all valid placements of <em>n </em>queens on an <em>n x n</em> board, using the representation discussed above. The output may be generated in any order you see fit. Your solution should be implemented as a depth-first search, where queens are successively placed in empty rows until all rows have been filled. <em>Hint: You may find it helpful to define a helper function </em>n_queens_helper(n, board)<em> that yields all valid placements which extend the partial solution denoted by </em>board<em>.</em></li>

</ol>

Though our discussion of search in class has primarily covered algorithms that return just a single solution, the extension to a generator which yields all solutions is relatively simple. Rather than using a return statement when a solution is encountered, yield that solution instead, and then continue the search.

&gt;&gt;&gt; solutions = n_queens_solutions(4)                                              &gt;&gt;&gt; list(n_queens_solutions(6))

&gt;&gt;&gt; next(solutions)                                                                                                                 [[1, 3, 5, 0, 2, 4], [2, 5, 1, 4, 0, 3],

[1, 3, 0, 2]                                                                                                                                    [3, 0, 4, 1, 5, 2], [4, 2, 0, 5, 3, 1]]

&gt;&gt;&gt; next(solutions)                                                                                            &gt;&gt;&gt; len(list(n_queens_solutions(8)))

[2, 0, 3, 1]                                                                                              92

<h1>2.   Lights Out [40 points]</h1>

The Lights Out puzzle consists of an <em>m x n</em> grid of lights, each of which has two states: on and off. The goal of the puzzle is to turn all the lights off, with the caveat that whenever a light is toggled, its neighbors above, below, to the left, and to the right will be toggled as well. If a light along the edge of the board is toggled, then fewer than four other lights will be affected, as the missing neighbors will be ignored.

In this section, you will investigate the behavior of Lights Out puzzles of various sizes by implementing a LightsOutPuzzle class. Once you have completed the problems in this section, you can test your code in an interactive setting using the provided GUI. See the end of the section for more details.

<ol>

 <li><strong>[2 points] </strong>A natural representation for this puzzle is a two-dimensional list of Boolean values, where True corresponds to the on state and False corresponds to the off state. In the LightsOutPuzzle class, write an initialization method __init__(self, board) that stores an input board of this form for future use. Also write a method get_board(self) that returns this internal representation. You additionally may wish to store the dimensions of the board as separate internal variables, though this is not required.</li>

</ol>

&gt;&gt;&gt; b = [[True, False], [False, True]]                                                   &gt;&gt;&gt; b = [[True, True], [True, True]]

&gt;&gt;&gt; p = LightsOutPuzzle(b)                                                                     &gt;&gt;&gt; p = LightsOutPuzzle(b)

&gt;&gt;&gt; p.get_board()                                                                                      &gt;&gt;&gt; p.get_board()

[[True, False], [False, True]]                                                                  [[True, True], [True, True]]

<ol start="2">

 <li><strong>[3 points] </strong>Write a top-level function create_puzzle(rows, cols) that returns a new LightsOutPuzzle of the specified dimensions with all lights initialized to the off state.</li>

</ol>

&gt;&gt;&gt; p = create_puzzle(2, 2)                                                                     &gt;&gt;&gt; p = create_puzzle(2, 3)

&gt;&gt;&gt; p.get_board()                                                                                      &gt;&gt;&gt; p.get_board()

[[False, False], [False, False]]          [[False, False, False],  [False, False, False]]

<ol start="3">

 <li><strong>[5 points] </strong>In the LightsOutPuzzle class, write a method perform_move(self, row, col) that toggles the light located at the given row and column, as well as the appropriate neighbors.</li>

</ol>

&gt;&gt;&gt; p = create_puzzle(3, 3)                                                                     &gt;&gt;&gt; p = create_puzzle(3, 3)

&gt;&gt;&gt; p.perform_move(1, 1)                                                                      &gt;&gt;&gt; p.perform_move(0, 0)

&gt;&gt;&gt; p.get_board()                                                                                      &gt;&gt;&gt; p.get_board()

[[False, True, False],                                                                                   [[True,  True,  False],

[True,  True, True ],                                                                                   [True,  False, False],

[False, True, False]]                                                                                   [False, False, False]]

<ol start="4">

 <li><strong>[5 points] </strong>In the LightsOutPuzzle class, write a method scramble(self) which scrambles the puzzle by calling perform_move(self, row, col) with probability <em>1/2</em> on each location on the board. This guarantees that the resulting configuration will be solvable, which may not be true if lights are flipped individually. <em>Hint: After importing the </em>random<em> module with the statement </em>import random<em>, the expression </em>random.random() &lt; 5<em> generates the values </em>True<em> and </em>False<em> with equal probability.</em></li>

 <li><strong>[2 points] </strong>In the LightsOutPuzzle class, write a method is_solved(self) that returns whether all lights on the board are off.</li>

 <li><strong>[3 points] </strong>In the LightsOutPuzzle class, write a method copy(self) that returns a new</li>

</ol>

LightsOutPuzzle object initialized with a deep copy of the current board. Changes made to the original puzzle should not be reflected in the copy, and vice versa.

&gt;&gt;&gt; p = create_puzzle(3, 3)                                                                     &gt;&gt;&gt; p = create_puzzle(3, 3)

&gt;&gt;&gt; p2 = p.copy()                                                                                        &gt;&gt;&gt; p2 = p.copy()

&gt;&gt;&gt; p.get_board() == p2.get_board()                                             &gt;&gt;&gt; p.perform_move(1, 1)

True                                                                                                                            &gt;&gt;&gt; p.get_board() == p2.get_board()

False

<ol start="7">

 <li><strong>[5 points] </strong>In the LightsOutPuzzle class, write a method successors(self) that yields all successors of the puzzle as (move, new-puzzle) tuples, where moves themselves are (row, column) tuples. The second element of each successor should be a new LightsOutPuzzle object whose board is the result of applying the corresponding move to the current board. The successors may be generated in whichever order is most convenient.</li>

</ol>

&gt;&gt;&gt; p = create_puzzle(2, 2)                                                                      &gt;&gt;&gt; for i in range(2, 6):

&gt;&gt;&gt; for move, new_p in p.successors(): …     p = create_puzzle(i, i + 1) …     print move, new_p.get_board() …     print len(list(p.successors()))

…           … (0, 0) [[True, True], [True, False]]              6

(0, 1) [[True, True], [False, True]]                                       12

(1, 0) [[True, False], [True, True]]                                       20

(1, 1) [[False, True], [True, True]]                                       30

<ol start="8">

 <li><strong>[15 points] </strong>In the LightsOutPuzzle class, write a method find_solution(self) that returns an optimal solution to the current board as a list of moves, represented as (row, column) tuples. If more than one optimal solution exists, any of them may be returned. Your solver should be implemented using a breadth-first graph search, which means that puzzle states should not be added to the frontier if they have already been visited, or are currently in the frontier. If the current board is not solvable, the value None should be returned instead. You are highly encouraged to reuse the methods defined in the previous exercises while developing your solution.</li>

</ol>

<em>Hint: For efficient testing of duplicate states, consider using tuples representing the boards of the </em>LightsOutPuzzle<em> objects being explored rather than their internal list-based representations. You will then be able to use the built-in </em>set<em> data type to check for the presence or absence of a particular state in near-constant time.</em>

&gt;&gt;&gt; p = create_puzzle(2, 3)                                                                         &gt;&gt;&gt; b = [[False, False, False],

&gt;&gt;&gt; for row in range(2):                                                                                   …      [False, False, False]]

…     for col in range(3):                                                                   &gt;&gt;&gt; b[0][0] = True

…         p.perform_move(row, col)                &gt;&gt;&gt; p = LightsOutPuzzle(b) …         &gt;&gt;&gt; p.find_solution() is None

&gt;&gt;&gt; p.find_solution()                                                                        True

[(0, 0), (0, 2)]

Once you have implemented the functions and methods described in this section, you can play with an interactive version of the Lights Out puzzle using the provided GUI by running the following command:

The arguments rows and cols are positive integers designating the size of the puzzle.

In the GUI, you can click on a light to perform a move at that location, and use the side menu to scramble or solve the puzzle. The GUI is merely a wrapper around your implementations of the relevant functions, and may therefore serve as a useful visual tool for debugging.

<h1>3.   Linear Disk Movement [30 points]</h1>

In this section, you will investigate the movement of disks on a linear grid.

The starting configuration of this puzzle is a row of <em>L</em> cells, with disks located on cells <em>0</em> through <em>n 1</em>. The goal is to move the disks to the end of the row using a constrained set of actions. At each step, a disk can only be moved to an adjacent empty cell, or to an empty cell two spaces away, provided another disk is located on the intervening cell. Given these restrictions, it can be seen that in many cases, no movements will be possible for the majority of the disks. For example, from the starting position, the only two options are to move the last disk from cell <em>n – 1</em> to cell <em>n</em>, or to move the second-to-last disk from cell <em>n – 2</em> to cell <em>n</em>.

<ol>

 <li><strong>[15 points] </strong>Write a function solve_identical_disks(length, n) that returns an optimal solution to the above problem as a list of moves, where length is the number of cells in the row and n is the number of disks. Each move in the solution should be a two-element tuple of the form (from, to) indicating a disk movement from the first cell to the second. As suggested by its name, this function should treat all disks as being identical.</li>

</ol>

Your solver for this problem should be implemented using a breadth-first graph search. The exact solution produced is not important, as long as it is of minimal length.

Unlike in the previous two sections, no requirement is made with regards to the manner in which puzzle configurations are represented. Before you begin, think carefully about which data structures might be best suited for the problem, as this choice may affect the efficiency of your search.

&gt;&gt;&gt; solve_identical_disks(4, 2)                                                              &gt;&gt;&gt; solve_identical_disks(4, 3)

[(0, 2), (1, 3)]                                                                                               [(1, 3), (0, 1)]

&gt;&gt;&gt; solve_identical_disks(5, 2)                                                              &gt;&gt;&gt; solve_identical_disks(5, 3)

[(0, 2), (1, 3), (2, 4)]                                                                                         [(1, 3), (0, 1), (2, 4), (1, 2)]

<ol start="2">

 <li><strong>[15 points] </strong>Write a function solve_distinct_disks(length, n) that returns an optimal solution to the same problem with a small modification: in addition to moving the disks to the end of the row, their final order must be the reverse of their initial order. More concretely, if we abbreviate length as <em>L</em>, then a desired solution moves the first disk from cell <em>0</em> to cell <em>L – 1</em>, the second disk from cell <em>1</em> to cell <em>L – 2</em>, <em>. . . </em>, and the last disk from cell <em>n – 1</em> to cell <em>L – n</em>.</li>

</ol>

Your solver for this problem should again be implemented using a breadth-first graph search.

As before, the exact solution produced is not important, as long as it is of minimal length.




&gt;&gt;&gt; solve_distinct_disks(4, 2)

[(0, 2), (2, 3), (1, 2)]

&gt;&gt;&gt; solve_distinct_disks(5, 2)

[(0, 2), (1, 3), (2, 4)]

&gt;&gt;&gt; solve_distinct_disks(4, 3) [(1, 3), (0, 1), (2, 0), (3, 2), (1, 3),

(0, 1)]

&gt;&gt;&gt; solve_distinct_disks(5, 3)




[(1, 3), (2, 1), (0, 2), (2, 4), (1, 2)]

<h1>4.   Feedback [5 points]</h1>

<ol>

 <li><strong>[1 point] </strong>Approximately how long did you spend on this assignment?</li>

 <li><strong>[2 points] </strong>Which aspects of this assignment did you find most challenging? Were there any significant stumbling blocks?</li>

 <li><strong>[2 points] </strong>Which aspects of this assignment did you like? Is there anything you would have changed?</li>

</ol>