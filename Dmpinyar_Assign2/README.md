# wyrm

GROUP MEMBERS: Devin Pinyard (dmpinyar), Kevin Alvarenga (kaalvare)

README instructions then documentation:

README:
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


Documentation:
One of my roommates, Jonathan, loves glizzies. Unfortunately, far too often, he misplaces his glizzies somewhere in the apartment. Now, the glizzy gobbler managed to lose his glizzies again, and he needs to find them. Now, he only needs one pack of glizzies, but somehow he’s managed to lose his entire supply of three glizzies! Further, he seems to have lost his tongs! He needs to find all of his glizzies, and then one of his pairs of tongs afterward (after all, he can’t pick up the glizzies if he has tongs in his hands)! They seem to have been lost in some especially dark corner of the apartment this time. Jonathan cannot find them on his own using his antediluvian searching techniques, so we must help Jonathan find them by communicating a traditional searching algorithm to him by yelling at him from across the apartment. Hopefully, Jonny will be able to prepare his glizzies with our help.


State definition: States are defined as various locations Jonathan can be in within the apartment, illustrated as a square grid composed of locations where he can stand and edges that he cannot pass through.
Initial state: The initial state is where Jonny starts in the search algorithm—in his bedroom. At this time, he will have no glizzies and no tongs in his possession.
Actions: The only actions Jonny can make are moving into an adjacent square not blocked off by an edge. The successor function will change the state into one where Jonny has moved to the chosen valid location.
Goal test: Has Jonny found all three glizzies? Did he just interact with the tongs after finding all three glizzies? Both need to be true concurrently.
Cost: The cost function will be how many steps it takes for him to optimally find the glizzies and tongs (so how many tiles are traversed in the search functions found path—only counts new tiles). 
Grid restrictions: he has to follow the layout of the apartment (cannot walk through walls).

The program prioritizes finding all three glizzies before it finds one of the goals. It then finds the path that does this optimally. This is all kind of done in the same step, but it all affects the cost function and the optimal cost found. 


Testing:
All directional path costs are 1 unless otherwise specified

(BFS)
Start State: 32
Hot Dogs: 62, 47, 82
Goals: 34, 48, 49
RESULTS
Number of expanded states: 220
Path length: 14
Total Path Cost: 13

Start State: 179
Hot Dogs: 62, 47, 82
Goals: 34, 48, 49
RESULTS
Number of expanded states: 120
Path length: 22
Total Path Cost: 21

Start State: 143
Hot Dogs: 62, 47, 82
Goals: 144, 77, 32
RESULTS
Number of expanded states: 122
Path length: 14
Total Path Cost: 13

Start State: 32
Hot Dogs: 62, 47, 82
Goals: 34, 48, 49
North Arc Cost: 1
South Arc Cost: 3
East Arc Cost: 1
West Arc Cost: 3
RESULTS
Number of expanded states: 220
Path length: 14
Total Path Cost: 25




(UCS)
Start State: 32
Hot Dogs: 62, 47, 82
Goals: 34, 48, 49
RESULTS
Number of expanded states: 220
Path length: 14
Total Path Cost: 13

Start State: 179
Hot Dogs: 62, 47, 82
Goals: 34, 48, 49
RESULTS
Number of expanded states: 120
Path length: 22
Total Path Cost: 21

Start State: 143
Hot Dogs: 62, 47, 82
Goals: 144, 77, 32
RESULTS
Number of expanded states: 122
Path length: 14
Total Path Cost: 13

Start State: 32
Hot Dogs: 62, 47, 82
Goals: 34, 48, 49
North Arc Cost: 1
South Arc Cost: 3
East Arc Cost: 1
West Arc Cost: 3
RESULTS
Number of expanded states: 260
Path length: 14
Total Path Cost: 25


Testing Reflection:
Breadth First Search seemed to branch out more and be more spread out across the entire environment. One of the most noticeable differences between the performance of the two algorithms was in the first test, where UCS missed the last glizzy (right next to the start) and went on a wild goose chase throughout the rest of the apartment, but BFS was able to find it right away. I can infer that the closer the three hot dogs and tongs were to the start, the more likely it was that the algorithm felt the need to explore the whole apartment. BFS failed in that it found the hot dogs just after exploring all the tongs, so it looked elsewhere before checking back. UCS failed in that it didn’t find all of the hot dogs fast enough, and had to come back to them toward the end in this situation. A* would likely outperform both because of the general knowledge of where the hot dogs and tongs would be—it wouldn’t be checking poor locations for them even remotely to the same extent. When the directional costs differed, UCS took significantly longer to determine the optimal state than BFS. This is likely due to it not realizing sooner that the optimal path was right at the beginning of it and requires some ostensibly suboptimal decisions to be made.
