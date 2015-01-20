hypercube-coloring
==================

This is a program to color the edges of a hypercube using the following rule (this rule can be modified by changing the ruleCheck function).  For a pair of non-adjacent vertices (v1,v2), it requires a  pair of "separating" (defined below) edges e1, e2 , of the same color, incident on v1, v2 respectively. Representing the vertices as binary strings, an edge  "separating position" for a pair of vertices is a position in which they differ. For instance, in a 3D cube, the vertices  v1=101 and v2=110,  are  "separated" in  positions 0 (LSB) and 1 (counting from right to left). A pair of parallel edges in a separating direction (LSB) would be, e1=(101,100)  incident on v1, and e2=(110,111) incident  on v2. The goal is to find a coloring that is maximal under the following  partial ordering of colorings. Assuming new colors are added from a fixed ordered set (necessarily finite), a coloring C1 is less than another coloring C2 if C1 can be obtained by identifying some of the colors in C2,  under symmetries of the hypercube. This algorithm has an initialization stage, and a coloring stage that recurs until either the algorithm succeeds in coloring the hypercube, or encounters a deadlock it cannot resolve, in which case it aborts. The initialization is done before calling the main "doColoring" routine.  For onitialization a user specifies and colors  a set of edges by calling methods within the hypercube object (with obvious names). The doColoring method chooses in a round-robin manner, a direction (0 to n-1) of the hypercube, picking a random uncolored edge in that direction and tries to color it with a new color. It checks to make sure the rule (constraint) is not violated  for each pair of vertices (locally, as opposed to globally, which would require checking if there are no conflicts between all such pairs) as a result of the added color. If nothing is inconsistent, it colors  those edges that must now be colored with one of the existent colors to be consitent with the rule. Then it moves to the next hypercube direction, and so on.  This is sort of a "greedy algorithm" (though not even locally optimal) in that it only looks at all pairs of vertices and ensures for each pair  the necessary conditions relevant to the pair. It does not guarantee that there are no conflicts between the pairs, which do arise and cause the program to abort. The algorithm implemented is probabilistic and each run yields (with a high probability), a successful coloring of the hypercube, though not always maximal. In general though, it seems to do a good job identifying a possible coloring each run. Needs improvement and generalization.

