### Abstract

* To explore how a few **graph algorithms** behave in the context of **mazes**



### Maze representation

* One dimensional
* Two dimensional



##### Method

* MazeExplorer
  * DFS
  * BFS

### DFS

```java
package lab11.graphs;

/**
 *  @author Josh Hug
 */
public class MazeDepthFirstPaths extends MazeExplorer {
    /* Inherits public fields:
    public int[] distTo;
    public int[] edgeTo;
    public boolean[] marked;
    */
    private int s;
    private int t;
    private boolean targetFound = false;
    private Maze maze;


    public MazeDepthFirstPaths(Maze m, int sourceX, int sourceY, int targetX, int targetY) {
        super(m);
        maze = m;
        s = maze.xyTo1D(sourceX, sourceY);
        t = maze.xyTo1D(targetX, targetY);
        distTo[s] = 0;
        edgeTo[s] = s;
    }

    private void dfs(int v) {
        marked[v] = true;
        announce();

        if (v == t) {
            targetFound = true;
        }

        if (targetFound) {
            return;
        }

        for (int w : maze.adj(v)) {
            if (!marked[w]) {
                edgeTo[w] = v;
                announce();
                distTo[w] = distTo[v] + 1;
                dfs(w);
                if (targetFound) {
                    return;
                }
            }
        }
    }

    @Override
    public void solve() {
        dfs(s);
    }
}
```



### BFS

```java
package lab11.graphs;

import java.util.ArrayDeque;
import java.util.Queue;

/**
 *  @author Josh Hug
 */
public class MazeBreadthFirstPaths extends MazeExplorer {
    /* Inherits public fields:
    public int[] distTo;
    public int[] edgeTo;
    public boolean[] marked;
    */
    private int s;
    private int t;
    private Maze maze;
    final int INFINITY = 99999;

    public MazeBreadthFirstPaths(Maze m, int sourceX, int sourceY, int targetX, int targetY) {
        super(m);
        // Add more variables here!
        maze = m;
        s = maze.xyTo1D(sourceX, sourceY);
        t = maze.xyTo1D(targetX, targetY);
        distTo[s] = 0;
        edgeTo[s] = s;
    }

    /** Conducts a breadth first search of the maze starting at the source. */
    private void bfs() {
        Queue<Integer> fringe = new ArrayDeque<>();
        for (int v = 1; v < maze.V(); v++) {
            distTo[v] = INFINITY;
        }
        marked[s] = true;
        announce();
        fringe.add(s);
        while (fringe.peek() != t) {
            int now = fringe.poll();
            for (int w: maze.adj(now)) {
                if (!marked[w]) {
                    edgeTo[w] = now;
                    distTo[w] = distTo[now] + 1;
                    marked[w] = true;
                    announce();
                    fringe.add(w);
                }
            }
        }
    }

    @Override
    public void solve() {
        bfs();
    }
}
```



### Issue

###### Debug

* Resume
* Conditional debugging





BFS --- Regular Queue FIFO

A* --- Priority Queue --compareable