# CSC520 Assignment 1 – Part 2

GROUP MEMBERS: Devin Pinyard (dmpinyar), Kevin Alvarenga (kaalvare)

# Analysis/Report

## Scenario
One of my roommates, Jonathan, loves hot dogs. Unfortunately, far too often, he misplaces his hot dogs somewhere in the apartment. Now, Jonathan managed to lose his hot dogs again, and he needs to find them. Now, he only needs one pack of hot dogs, but somehow he’s managed to lose his entire supply of three hot dogs! Further, he seems to have lost his tongs! He needs to find all of his hot dogs, and then one of his pairs of tongs afterward (after all, he can’t pick up the hot dogs if he has tongs in his hands)! They seem to have been lost in some especially dark corner of the apartment this time. Jonathan cannot find them on his own using his antediluvian searching techniques, so we must help Jonathan find them by communicating a traditional searching algorithm to him by yelling at him from across the apartment. Hopefully, Jonny will be able to prepare his hot dogs with our help.

## Testing
All directional path costs are 1 unless otherwise specified. We chose “three different starting states” for our testing. We included a fourth test case that uses different edge weights as an additional test for cost comparison. 

### Breadth-First Search (BFS)
We report edge weight costs for BFS to show a comparison in solution cost with UCS, even though BFS doesn’t use the edge weights. BFS uses a FIFO (queue) approach. 

| Test Case | Expanded States | Path Length | Total Path Cost |
|------------|----------------|-------------|-----------------|
| Start: 32<br>Hot Dogs: 62, 47, 82<br>Goals: 34, 48, 49 | 220 | 14 | 13 |
| Start: 179<br>Hot Dogs: 62, 47, 82<br>Goals: 34, 48, 49 | 120 | 22 | 21 |
| Start: 143<br>Hot Dogs: 62, 47, 82<br>Goals: 34, 48, 49 | 120 | 14 | 13 |
| Start: 32<br>Hot Dogs: 62, 47, 82<br>Goals: 34, 48, 49<br>North Arc Cost: 10, South Arc Cost: 1, East Arc Cost: 10, West Arc Cost: 1 | 220 | 14 | 76 |


### Uniform Cost Search (UCS)

UCS was implemented using a priority queue to optimize accumulated costs, `g(n)`.

| Test Case | Expanded States | Path Length | Total Path Cost |
|------------|----------------|-------------|-----------------|
| Start: 32<br>Hot Dogs: 62, 47, 82<br>Goals: 34, 48, 49 | 220 | 14 | 13 |
| Start: 179<br>Hot Dogs: 62, 47, 82<br>Goals: 34, 48, 49 | 120 | 22 | 21 |
| Start: 143<br>Hot Dogs: 62, 47, 82<br>Goals: 34, 48, 49 | 120 | 14 | 13 |
| Start: 32<br>Hot Dogs: 62, 47, 82<br>Goals: 34, 48, 49<br>North Arc Cost: 10, South Arc Cost: 1, East Arc Cost: 10, West Arc Cost: 1 | 222 | 14 | 76 |

### Testing Reflection / Analysis
Across the first three test cases, where all directional edge costs were equal to 1, BFS and UCS gave identical solution paths, lengths, and total path costs. This was expected since when all edge costs are uniform, minimizing the number of actions (BFS) would be the same as minimizing accumulated cost,`g(n)`, which is UCS. Therefore, both algorithms expanded the same number of states here, showing that UCS can be the same as BFS under the constraint of uniform edge costs. However, we did notice some differences in the weighted test case (case 4), where North and East directions had an edge cost of 10, and South and West had an edge cost of 1. Both algorithms gave the same solution path and total cost, which means that for our current graph design, the lowest cost solution also happened to be the same as the shortest-step solution. This is mostly due to the walls and layout of our graph restricting certain areas and the placement of the hot dogs and tongs (goals). While both algorithms did provide the same solution, UCS expanded slightly more states, 222, while BFS expanded 220. This reflects the additional steps required by UCS to prioritize by cumulative cost and optimize path cost. On the otherhand, BFS just focused on the order of depth and doesn’t take into account the edge weights for its search order. 

From these results, we can infer that UCS will be advantageous in scenarios where action costs vary more and if there is a longer path that has a lower total cost than a shorter path. Our current graph design did not provide this tradeoff due to the restrictive nature of the walls and placement of items. In these cases, BFS could return a suboptimal solution since it doesn’t take into account edge weights. If we were to implement A* instead, we would see a reduction in the number of states expanded while optimizing cost. This would be possible if we had an admissible heuristic, `h(n)`, that prioritized states that were closer to hot dogs and a goal. 


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


