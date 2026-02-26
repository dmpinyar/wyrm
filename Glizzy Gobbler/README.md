# wyrm

To run: import it in the SNAP! website and click the run button. Do not mess with the step meter, the character waits .1 seconds between steps, but the graph initialization code takes too long to run, so don't even mess with the step meter.

Code is encapsulated within little blocks. Most of which are all in the variables tab. The graph data structure holds a list of functionally structs holding a node and a corresponding list of arcs to take and their path cost. Initialization code for the graph converts a binary map into the graph data structure for traversal.
Other than that, all variables are named reasonably, so to test just open their visual and run the program.

To select which algorithm to run just swap the two grey blocks in the player characters sprite code. There is one for UCS, one for BFS.

To configure test cases just modify the values inside of these grey blocks. UCS uses UCS algorithm, BFS uses BFS algorithm. The number next to it represents the starting state.
Tongs represent goal states, and the number is the position corresponding to its state
Hotdogs represent required pickups, and the number is the position corresponding to its state
All states are representing by a mapping of a linear position to an x-y position. The actual formula we used is N = 15y + x, from y top down, x left right, but all lists are 1 indexed, so the first top left valid position ends up being 32 incrementing by 1 to the right, and incrementing by 15 downwards.

To view outputs display corresponding variables and read it after running. Relevant ones for test case include Expand, ExpandCount, Graph, Fringe, Goals, Hotdogs, SolutionPath, and Visited.

Jonny cannot travel through walls and he has the superpower to teleport to states he is actively checking instead of needing to walk all the way to them, but the found path ends up being one that follows all natural limitations.