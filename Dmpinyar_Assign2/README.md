# wyrm

GROUP MEMBERS: Devin Pinyard (dmpinyar), Kevin Alvarenga (kaalvare)


# CSC520 Assignment 1 – Part 2

# Analysis/Report

## Scenario
One of my roommates, Jonathan, loves hot dogs. Unfortunately, far too often, he misplaces his hot dogs somewhere in the apartment. Now, Jonathan managed to lose his hot dogs again, and he needs to find them. Now, he only needs one pack of hot dogs, but somehow he’s managed to lose his entire supply of three hot dogs! Further, he seems to have lost his tongs! He needs to find all of his hot dogs, and then one of his pairs of tongs afterward (after all, he can’t pick up the hot dogs if he has tongs in his hands)! They seem to have been lost in some especially dark corner of the apartment this time. Jonathan cannot find them on his own using his antediluvian searching techniques, so we must help Jonathan find them by communicating a traditional searching algorithm to him by yelling at him from across the apartment. Hopefully, Jonny will be able to prepare his hot dogs with our help.

## Testing
All directional path costs are 1 unless otherwise specified. We chose “three different starting states” for our testing. We included a fourth test case that uses different edge weights as an additional test for cost comparison. 

### BFS


# README

## 1. How to Open and Run the SNAP Project
1. Open the SNAP website
2. Import the project file:
3. Click the green flag to run the program.
4. Please do not modify the step meter. The sprite is set to wait 0.1 seconds in between expansions. Also the graph may take a few seconds to set up before the search animation begins.

## 2. Infrastructure Design
### Graph Representation
The environment is represented as a state-space graph that is constructed from a binary grid matrix. 
- Each valid grid location tile represents a node
- Each node has a list of neighbors.
- Each neighbor is represented as list: [node, cost/edge weight]
You are capable of editing the graph structure by editing the binary map/grid or edge costs. Therfore, you do not need to modify the search algoritms.

### State Representation
Each state has the following: 
- Position (index from the grid)
- Bitmask which indicates the hot dogs collected

### Transition Function
Successor Function: 
- Generated adjacent valid moves (go north, east, south, west)
- Applies the edge weight to those moves
- Updates the bitmask for hot dog collection

### How We Handle Costs
- We store edge costs in the graph
- We keep track of g(n) during the search, which is the accumulated cost.
- BFS uses a queue (FIFO) to expand and determine order, which is just depth.
- UCS prioritizes the next state by using g(n).

## Search Engine 
We implemented two search algorithms: 
- BFS: Uses a queue (FIFO)
- UCS: Uses a priority queue that is ordered by g(n).

To switch between the two algorithms: 
You must be in the player sprite script, and replace the BFS gray custom block with the UCS gray custom block, or vice versa. 

Each algorithm contains a starting state, hot dog locations, goal states (the tongs), and optional directional edge costs. 

To modify a test case: 
- For directional edge weight changes: Adjust the values that directionArcCost are set to.
- To change hot dog locations: Adjust the value in the add hotdog blocks.
- To change the goal/tong locations: Adjust the value in the add goal blocks.

## Outputs Produced 
After running one of the search algorithms, you will see the following variables on the screen:
- SolutionPath: This is a list of the solution path the algorithm returned.
- currCost: This is the solution cost, the total path cost.
- ExpandCount: The number of states expanded.
- Expand: The list of states expanded.
- Graph: The list represenation of the graph.
- Fringe: List of states currently stored in the fringe.

All of these variables can be turned on/off with the little checkmark box in the variables category (left side). 

## Assumptions/Limitations
- The agent/sprite isn't capable of passing through the walls or going on unwalkable tiles (non-orange tiles).
- For visualization purposes, the sprite teleports to the state it is expanding/visiting.
- We need to keep edge costs non-negative for UCS.
- We did not implement A* in this project, so there is no h(n), admissible heuristic. 


