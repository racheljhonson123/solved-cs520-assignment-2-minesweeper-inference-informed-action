Download Link: https://assignmentchef.com/product/solved-cs520-assignment-2-minesweeper-inference-informed-action
<br>
This project is intended to explore how data collection and inference can inform future action and future data collection. This is a situation frequently confronted by artificial intelligence agents operating in the world – based on current information, they must decide how to act, balancing both achieving a goal and collecting new information. Additionally, this project stresses the importance of formulation and representation. There are a number of roughly equivalent ways to express and solve this problem, it is left to you to decide which is best for your purposes.

<h1>1         Background: MineSweeper</h1>

In the game minesweeper, you are presented with a square grid landscape of cells. Hidden in some of the cells are ‘mines’. At every turn, you may select a cell to uncover. At this point, one of two things will happen: if there is a mine at that location, it explodes and you lose the game; if there is not a mine at that location, it reveals a number, indicating the number of adjacent cells where there are mines. If the cell reveals 0, all the surrounding 8 cells are empty of mines. If the cell reveals 8, all 8 adjacent cells must have mines. For any value in between, for instance 4, you know that half of the adjacent cells have mines, but you cannot be sure by this clue alone which half are dangerous and which half are safe.

The goal of the game is to identify the locations of all the mines (if possible); by collecting clues and information, you can begin to infer which cells are dangerous and which are safe, and use the safe cells to collect more information. This process is iterated until, hopefully, all cells are either uncovered, marked as clear, or marked as mined.

Figure 1: In the first board, all cells are unknown. The first move reveals a 3, in which case we may infer that all three surrounding cells have mines. We mark them as such, and know not to ever search those cells. The second move reveals a 0, in which case we know that all 8 surrounding cells must be clear. We mark them as clear, and know that we can search them without worry. Collecting data from the clear cells, we are able to infer the locations of more mines.

The goal of this project is to write a program to play MineSweeper – that is, a program capable of sequentially deciding what cells to check, and using the resulting information to direct future action.

<h1>2         Program Specification</h1>

Your program should initially meet the following specifications for use (though some modifications and suggestions are given in the questions for writeup). The user should have a board / distribution of mines in mind, and use it to answer the program’s queries.

<ul>

 <li>Initially take input from the user, specifying the length and width of the board, then enter the following loop:</li>

 <li>Display a representation of the current state of knowledge about the board (unknown cells, clear cells, mine cells, clue cells).</li>

 <li>Query the user for the state of a specified cell based on its coordinates. If the cell has no mine, the user should enter a number between 0 and the number of adjacent cells, specifying the number of adjacent mines. If the cell has a mine, the user should enter this, at which point the game is over and the computer has lost.</li>

 <li>The game finishes once either a) the computer accidentally queried a mine cell, or b) all cells have been either revealed, or marked as clear / mined.</li>

</ul>

You may either do a GUI or a text based interface – the important thing in either case is accurately displaying the current state of the program’s knowledge. Very deliberately, there are no algorithmic specifications for how to implement this program. But you should draw on the material discussed both in a) Search, b) Constraint-Satisfaction Problems, and c) Logic and Satisfiability. As usual, you must create your own code for solving the main issues and algorithmic problems in this assignment, but you are welcome to use external libraries for things like visualizations, etc.

<h1>3         Questions and Writeup</h1>

Answer the following questions about the design choices you made in implementing this program, both from a representational and algorithmic perspective.

<ul>

 <li>Representation: How did you represent the board in your program, and how did you represent the information / knowledge that clue cells reveal?</li>

 <li>Inference: When you collect a new clue, how do you model / process / compute the information you gain from it? i.e., how do you update your current state of knowledge based on that clue? Does your program deduce everything it can from a given clue before continuing? If so, how can you be sure of this, and if not, how could you consider improving it?</li>

 <li>Decisions: Given a current state of the board, and a state of knowledge about the board, how does your program decide which cell to search next? Are there any risks, and how do you face them?</li>

 <li>Performance: For a reasonably-sized board and a reasonable number of mines, include a play-by-play progression to completion or loss. Are there any points where your program makes a decision that you don’t agree with? Are there any points where your program made a decision that surprised you? Why was your program able to make that decision?</li>

 <li>Performance: For a fixed, reasonable size of board, what is the largest number of mines that your program can still usually solve? Where does your program struggle?</li>

 <li>Efficiency: What are some of the space or time constraints you run into in implementing this program? Are these problem specific constraints, or implementation specific constraints? In the case of implementation constraints, what could you improve on?</li>

 <li>Improvements: Consider augmenting your program’s knowledge in the following way – when the user inputs the size of the board, they also input the total number of mines on the board. How can this information be modeled and included in your program, and used to inform action? How can you use this information to effectively improve the performance of your program, particularly in terms of the number of mines it can effectively solve.</li>

</ul>

<h1>4         Bonus: Chains of Influence</h1>

For any cell that is marked clear or mined, we can think about the cells that led to or informed that conclusion. In Fig. 1 above, Cell (0<em>,</em>0) [upper left corner] containing the clue 3 is enough to determine the value of Cells (1<em>,</em>0)<em>,</em>(1<em>,</em>1)<em>,</em>(0<em>,</em>1). Cell (1<em>,</em>2) on the other hand (depending on your specific implementation) depended on Cell (2<em>,</em>4) which revealed the values of Cell (1<em>,</em>4) and Cell (1<em>,</em>3) – these, combined with the clue in Cell (2<em>,</em>3), was enough to mark the value of Cell (1<em>,</em>2) as clear.

In this way, for every cell we can determine the value of, we can construct a chain of influence that led to the marking – starting at revealed cells, cells those allowed to be marked, and working through the chain of inference to the conclusion for the value of a certain cell. Every new cell will inherit the chain of influence of any cell that influenced it – you can imagine this as a very large directed acyclic graph branching out from the initial cell you reveal (or any unjustified / guessed cell you reveal).

<ul>

 <li>Based on your model and implementation, how can you characterize and build this chain of influence? <em>Hint:</em></li>

</ul>

<em>What are some ‘intermediate’ facts along the chain of influence?</em>

<ul>

 <li>What influences or controls the length of the longest chain of influence when solving a certain board?</li>

 <li>How does the length of the chain of influence influence the efficiency of your solver?</li>

 <li>Can you find a board that yields particularly long chains of influence? How does this vary with the total number of mines?</li>

 <li>Spatially, how far can the influence of a given cell travel?</li>

 <li>Can you use this notion of minimizing the length of chains of influence to inform the decisions you make, to try to solve the board more efficiently?</li>

 <li>Is solving minesweeper hard?</li>

</ul>

<h1>5         Bonus: Dealing with Uncertainty</h1>

In real world situations, you are frequently confronted with incomplete or partial information. Three possible models of that here might be:

<ul>

 <li>When a cell is selected to be uncovered, if the cell is ‘clear’ you only reveal a clue about the surrounding cells with some probability. <em>In this case, the information you receive is accurate, but it is uncertain when you will receive the information.</em></li>

 <li>When a cell is selected to be uncovered, the revealed clue is less than or equal to the true number of surrounding mines (chosen uniformly at random). <em>In this case, the clue has some probability of underestimating the number of surrounding mines. Clues are always optimistic.</em></li>

 <li>When a cell is selected to be uncovered, the revealed clue is greater than or equal to the true number of surrounding mines (chosen uniformly at random). <em>In this case, the clue has some probability of overestimating the number of surrounding mines. Clues are always cautious.</em></li>

</ul>

How could you adapt your solver to each of these three cases? Try to implement at least one, and experiment with what kind of performance hit results, in terms of ability to clear the board.