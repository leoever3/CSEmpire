### Abstract

* Artificial Intelligence
* Solve puzzles
  * Take the given world state and find a sequence of valid transitions between world states such that puzzle is solved
* solution to **any WorldState puzzle**
* Shortest possible solution

###### Priority queue



### Best-First Search

1. ##### Define search node -- WorldState

2. ##### Priority queue



#### Task 1

* WorldState
  * Distance to goal -- int
  * neighbours -- iterable
  * Is goal? -- boolean



###### optimization

* Grandpa
* Save the computed value



### Some Codes

```java
package hw4.puzzle;

import edu.princeton.cs.algs4.MinPQ;

import java.util.ArrayDeque;
import java.util.Deque;


public class Solver {
    private int moves;
    private SearchNode searchNode;
    private MinPQ<SearchNode> pq = new MinPQ<>();
    private Deque<WorldState> solution = new ArrayDeque<>();


    private class SearchNode implements Comparable<SearchNode> {
        WorldState worldState;
        int move;
        SearchNode previous;
        int distance;
        SearchNode(WorldState ws, int m, SearchNode p) {
            worldState = ws;
            move = m;
            previous = p;
            if (ws == null) {
                distance = 0;
            } else {
                distance = m + ws.estimatedDistanceToGoal();
            }
        }
        public int compareTo(SearchNode s) {
            return this.distance - s.distance;
        }
    }


    /* Constructor which solves the puzzle, computing
     * everything necessary for moves() and solution() to
     * not have to solve the problem again. Solves the
     * puzzle using the A* algorithm. Assumes a solution exists.*/
    public Solver(WorldState initial) {
        searchNode = new SearchNode(initial, 0, null);
        pq.insert(searchNode);
        SearchNode x = pq.delMin();
        SearchNode grandpa = new SearchNode(null, 0, null);
        while (!x.worldState.isGoal()) {
            for (WorldState w : x.worldState.neighbors()) {
                if (!w.equals(grandpa.worldState)) {
                    SearchNode s = new SearchNode(w, x.move + 1, x);
                    pq.insert(s);
                }
            }
            x = pq.delMin();
            grandpa = x.previous;
        }
        moves = x.move;
        while (x.previous != null) {
            solution.addFirst(x.worldState);
            x = x.previous;
        }
        solution.addFirst(initial);
    }

    /* returns the minimum number of moves to solve the puzzle starting
     * at the initial WorldState. */
    public int moves() {
        return moves;
    }

    /* Returns a sequence of WorldStates from the initial WorldState
     * to the solution. */
    public Iterable<WorldState> solution() {

        return solution;
    }
}

```

### A*

* Hamming -- at least Hamming moves
* Manhattan -- each tile must move it's Manhattan distance





### Issues

##### Equals!!!!! not ==



###### Interface

* Word implements interface WorldState
  * We need to find the variable in Class Word but not Interface WorldState



###### Set the command line arguments

* Edit configurations