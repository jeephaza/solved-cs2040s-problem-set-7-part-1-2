Download Link: https://assignmentchef.com/product/solved-cs2040s-problem-set-7-part-1-2
<br>
<h1>Problem 7.             (Mazes are Just Dynamite! Part 1)</h1>

It’s easy to get lost in life. In this series of problem sets, we’re going to develop a program to help us get unlost. Even better, we’re going to give you some extra superpowers: the ability to break down the obstacles in your way, helping you to get to your destination even faster.

To start off for now, you are given a map of the maze you are lost in. Like most mazes, this maze consists of one or more rooms. Each of the rooms has doors to one or more other rooms. Your first job is to write a program that will explore the maze, as is, and discover the shortest path from your current location to a destination location. Simultaneously, your program will be expected to determine some other geographic information about the maze.

We’ll talk about your superpowers later in part 2 of this problem set series.

<strong>Preliminaries. </strong>We have provided you with some basic framework code for handling the maze. A maze consists of an <em>r </em>× <em>c </em>grid of rooms, with adjacent rooms separated by either a wall or an empty space. Furthermore, the entire maze is bordered by walls.

The rooms are numbered starting from the top left corner (which is (0<em>,</em>0)). The first coordinate specifies the row number, and the second coordinate specifies the column number. For example, in a 5 × 5 maze, the bottom left corner is (4<em>,</em>0) and the top right corner is (0<em>,</em>4).

Here is a pictorial example of a 5 × 5 maze:

0 1 2 3 4

###########

<ul>

 <li>#R R R#R#R#</li>

</ul>

### # # # #

<ul>

 <li>#R#R#R R R#</li>

</ul>

# ### ### #

<ul>

 <li>#R R R#R R#</li>

</ul>

# ### # # #

<ul>

 <li>#R#R R#R#R#</li>

</ul>

# # # ### #

<ul>

 <li>#R#R#R#R R# ###########</li>

</ul>

In this diagram, each wall is depicted using a hash symbol, i.e., #, while each room is depicted using the letter R (this is for visualization purposes only – in the actual maze files, the rooms are represented as empty spaces as well!). Notice that there are exactly <em>c </em>rooms and at most <em>c </em>+ 1 walls (including the left and right borders) on each row.

You may move between adjacent rooms in any of the four cardinal directions (north, south, east and west) if there is no wall in that direction. Diagonal movement is not allowed. In the above example, one can move from (0,0) to (0,1), but <strong>NOT </strong>from (0,0) to (1,0), nor from (0,0) to (1,1). ###########

#PPPPP# # #

### #P# # #

# # #PPPPP#

# ### ###P#

#              # P#

# ### # #P#

# #         # #P#

# # # ###P#

# # # # P#

###########

<strong>Figure 1: </strong>Example printMaze output of a solved maze

We provide you with two classes Maze and Room that represent the maze that your program will solve. The size of the maze is represented by the number of <em>rows </em>and <em>columns </em>in the maze (in the above example, both <em>rows </em>and <em>columns </em>are 5). The maze itself is represented by a matrix of rooms. You will be able to check if there exists a wall in the four directions of the room through the public methods hasNorthWall(), hasSouthWall(), hasEastWall() and hasWestWall(). On top of that, there is a public boolean attribute onPath that you can set for each room (for printing of mazes).

The Maze class has a static method readMaze(String fileName) that reads in a maze from a text file and returns the maze object. We have provided several sample mazes for you to experiment with. We also provide a simplistic way of visualizing a maze through the static class MazePrinter.

The static method void printMaze(Maze maze) of the MazePrinter class prints out a maze to the standard output<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>, as per the example in Figure 1.

We also provide you with the class ImprovedMazePrinter which prints out a much prettier version of the maze. (It was contributed by a former student: Mai Anh Vu.)

<strong>In this problem set, you will implement the class </strong>MazeSolver <strong>that will implement the provided interface </strong>IMazeSolver<strong>.</strong>

<h1>Problem 7.a.           The Average Coder</h1>

Joe the Average Coder is eager to solve this problem and implemented the class MazeSolverNaive (found in <em>MazeSolverNaive.java</em>). In particular, Joe implemented the pathSearch method that will return the <strong>minimum </strong>number of steps to get from a given starting coordinate to a target coordinate. He did so using the <strong>Depth-First Search </strong>traversal that he learned in his Algorithms and Data Structures class.

Take a look at Joe’s code. Given an arbitrary maze, will his algorithm find the shortest path from the start to the target? Why or why not? (You do not need to submit any code here. Just explain your answer.)

<h1>Problem 7.b.           Exploring the Maze</h1>

Now implement the class MazeSolver that correctly implements the IMazeSolver interface. First, implement the method:

Integer pathSearch(int startRow, int startCol, int endRow, int endCol)

which searches for the shortest path from the specified start room to the specified end room. It should return an integer representing the minimum number of steps needed if a path is found, or null if no such path is available. When your search is complete, we should have that R.onPath == true for every room <em>R </em>on the path and R.onPath == false for every room <em>R </em>not on the path. If done correctly, you will be able to execute printMaze(Maze maze) after your search is completed to draw the path taken by the solver, as in Figure 1.

Next, implement the method: Integer numReachable(int k) that will return an integer indicating how many rooms there are such that the <strong>minimum </strong>number of steps required to reach it is <em>k</em>, based on your most recent pathSearch starting location. Your numReachable method should count the number of rooms reachable from the initial location for each possible number of steps. For example, how many rooms are there with a minimum path distance of 0? How many rooms are reachable with minimum 1 step? How many rooms are reachable with minimum 2 steps? etc. For the example maze shown in Figure 1, with the most recent pathSearch start location being (0,0), the following holds (on the next page):

<ul>

 <li>Step: 1 Room</li>

 <li>Step: 1 Room</li>

 <li>Steps: 2 Rooms</li>

 <li>Steps: 1 Room</li>

 <li>Steps: 2 Rooms</li>

 <li>Steps: 4 Rooms</li>

 <li>Steps: 5 Rooms</li>

 <li>Steps: 5 Rooms</li>

 <li>Steps: 3 Rooms</li>

 <li>Steps: 1 Room</li>

</ul>

Notice that for each <em>k</em>, it outputs the number of rooms for which the minimum path distance is <em>k </em>exactly. If you calculate this for every initial starting point in the maze, then you can determine the <em>diameter </em>of the maze.

Your numReachable method should be <strong>efficient</strong>, as it will likely be called several times after a pathSearch.

<h1>Problem 7.c.            Maze Generation (Optional)</h1>

Sometimes you need to escape a maze, sometimes you need to build one<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>. In this problem, we would like to implement an algorithm for generating a maze. To get started, you may wish to read through this interesting review of various maze generation algorithms:

<a href="http://weblog.jamisbuck.org/2011/2/7/maze-generation-algorithm-recap">http://weblog.jamisbuck.org/2011/2/7/maze-generation-algorithm-recap</a>

This blog entry summarizes 11 different methods for generating a maze. All of these techniques yield mazes that have only one route from start to finish (i.e., there are no cycles—they generate a tree). You might think about how to modify them to generate interesting graphs/mazes that have more than one possible solution.

Inside the MazeGenerator class, implement the following method:

Maze generateMaze(int rows, int columns).

It should return a randomly generated maze given the number of rows and columns we would like the maze to contain. If you feel that it will make the generated mazes more interesting, feel free to add or remove parameters from the generateMaze method.

Submit your MazeGenerator class, along with a discussion of the design decisions that you made, and your favorite maze that was generated by the algorithm (with no manual intervention).

<a href="#_ftnref1" name="_ftn1">[1]</a> For an additional zero extra bonus points, implement a prettier graphical maze display and share it with the rest of the class.

<a href="#_ftnref2" name="_ftn2">[2]</a> See, for example, <em>Inception </em>(2010).