##### Part 1 Meet the Tile Rending Engine

### Abstraction

Two main file

* Draw a world
* Generate randomness



### Reading part

* **API (application programming interface)**

##### Boring World

1. Creating **TERenderer** object

   Initialize

​		Pixel 像素 16 * 16

2. **Tetile** objects 
   1. TETile constructer -- TETile.java
   2. Tileset.java
      1. WALL
      2. FLOWER ...
3. **Draw** the world



##### Ramdom World

* **Radom class** -- pseudorandom numbers 伪随机数
  * get different sequences by choosing seed
  * same seed generates same sequence
  
* **Switch**
* **Delegates work to functions with clearly defined behavior**



##### Doing part:

* Use the Tile Rendering Engine

* Define private helper method

1. `addHexagon`
2. `draw`
3. `calculate quantities` *2
4. JUnit test

###### Josh Hint

public static void addHexagon(TETile[][] world, Position p, int s, TETile t), where Position is a very simple class with two variables p.x and p.y and no methods. p specifies the lower left corner of the hexagon.

###### Josh thought

First: I wrote a couple of methods that compute the bottom-left Position of a current hexagon’s neighbors. For example, I wrote topRightNeighbor, which computed the right thing to pass to addHexagon so that I could get my topRight neighbor. I did not write JUnit tests for this because I knew it’d be easy to visually test, though JUnit tests would have been fine. I then wrote bottomRight, and ended up with 3 whole hexagons out of the 19 I wanted.

Second: I tried to figure out how I could use bottomRight and topRight in some clever way to get the whole grid, but was a bit stymied. I considered trying to use recursion in some way, but it didn’t feel like the right solution for symmetry reasons (too much weird backtracking). I then thought about whether I’d be stuck having to write six different neighbor methods, and decided that seemed excessive. All of this was done without any coding. If I’d have started coding all this, it would have been a huge waste of time.”

Third: Stepping back, I decided to try to find the “nicest” way to try to lay out my hexagons and was ready to throw away my bottomRight and topRight methods entirely. Then the key AHA moment occurred when I noticed that the world consists of 5 columns of 3, 4, 5, 4, and 3 hexagons, respectively.

Fourth: I wrote a method called drawRandomVerticalHexes that draws a column of N hexes, each one with a random biome.

Fifth: I wrote a main method that is a little ugly, but basically calls drawRandomVerticalHexes five times, one for each of the five columns of the world, consisting of 3, 4, 5, 4, and 3 hexagons. To figure out the starting position for the “top” hex of each column, I used the topRightNeighbor or bottomRightNeighbor on the old top, as appropriate.

Sixth: I added some code to allow for interactivity so you can press a single key to get a new random world and enjoyed playing around with it. But interactivity will have to wait until next week’s lab for you guys.



* **Recursion**
* **Abstraction**
  * Specific job

#### Idea:

1. **Position class (p.x, p.y)**
2. **Initial filling the board with nothing**
3. **Draw a row**
4. **Draw hexegon row by row using recursion in helper method**
5. **fill the hexegon by random tile**
6. **Draw a colomn of hexegon**
7. **Draw the world column by column**

```java
package byog.lab5;
import org.junit.Test;
import static org.junit.Assert.*;

import byog.TileEngine.TERenderer;
import byog.TileEngine.TETile;
import byog.TileEngine.Tileset;

import java.util.Random;

/**
 * Draws a world consisting of hexagonal regions.
 *
 * addHexagon
 * drawing
 * calculate the total level
 * calculate the position
 */
public class HexWorld {
    private static final int WIDTH = 28;
    private static final int HEIGHT = 30;

    private static final long SEED = 2873121;
    private static final Random RANDOM = new Random(SEED);

    private static class Position{
        int x;
        int y;

        Position (int x, int y) {
            this.x = x;
            this.y = y;
        }

        public Position shift(int dx, int dy) {
            return new Position(this.x + dx, this.y + dy);
        }
    }

    /**
     * Fills the given 2D array of tiles with RANDOM tiles.
     * @param tiles
     */
    public static void fillBoardWithNothing(TETile[][] tiles) {
        int height = tiles[0].length;
        int width = tiles.length;
        for (int x = 0; x < width; x += 1) {
            for (int y = 0; y < height; y += 1) {
                tiles[x][y] = Tileset.NOTHING;
            }
        }
    }
    /**
     * Draws a row of tiles anchored at a given position
     */
    public static void drawRow(TETile[][] tiles, Position p, TETile tile, int length) {
        for (int dx = 0; dx < length; dx += 1) {
            tiles[p.x + dx][p.y] = tile;
        }
    }
    /**
     * Helper method for addHexagon in recursion
     */
    private static void addHexagonHelper(TETile[][] tiles, Position p, TETile tile, int b, int t) {
        // Draws the row
        Position startOfRow = p.shift(b, 0);
        drawRow(tiles, startOfRow, tile, t);
        // Draws the remaining rows recursively
        if (b > 0) {
            Position nextP = p.shift(0, -1);
            addHexagonHelper(tiles, nextP, tile, b - 1, t + 2);
        }
        // Draws tje reflection's row
        Position startOfReflectionRow = startOfRow.shift(0, - (2 * b + 1));
        drawRow(tiles, startOfReflectionRow, tile, t);
    }

    /**
     * Adds a hexagon to the world at Position p of Size s
     */
    public static void addHexagon(TETile[][] tiles, Position p, TETile tile, int size) {
        if (size < 2) {
            return;
        }
        addHexagonHelper(tiles, p, tile, size - 1, size);
    }

    /** Picks a RANDOM tile with a 33% change of being
     *  a wall, 33% chance of being a flower, and 33%
     *  chance of being empty space.
     */
    private static TETile randomTile() {
        int tileNum = RANDOM.nextInt(5);
        switch (tileNum) {
            case 0: return Tileset.GRASS;
            case 1: return Tileset.FLOWER;
            case 2: return Tileset.SAND;
            case 3: return Tileset.MOUNTAIN;
            case 4: return Tileset.TREE;
            default: return Tileset.NOTHING;
        }
    }
    /**
     * Add a column of Hexagons
     */
    public static void addHexColum(TETile[][] tiles, Position p, int size, int num) {
        if (num < 1) {
            return;
        }
        addHexagon(tiles, p, randomTile(), 3);
        Position bottomNeighbor = p.shift(0 , - size * 2);
        addHexColum(tiles, bottomNeighbor, size, num - 1);
    }



    /**
     * Draws the hexagonal world
     */
    public static void drawWorld(TETile[][] tiles, int hexSize, int tessSize) {
        Position p = new Position(0, hexSize * 2 * (tessSize + 1)- 1);
        for (int i = 0; i < tessSize; i ++) {
            addHexColum(tiles, p, hexSize, tessSize + i);
            p = p.shift(2 * hexSize - 1, hexSize);
        }
        p = p.shift(0, - 2 * hexSize);
        for (int i = tessSize - 2; i >= 0; i --) {
            addHexColum(tiles, p, hexSize, tessSize + i);
            p = p.shift(2 * hexSize - 1,  - hexSize);
        }
    }

    public static void main(String[] args) {
        TERenderer ter = new TERenderer();
        ter.initialize(WIDTH, HEIGHT);

        TETile[][] world = new TETile[WIDTH][HEIGHT];
        fillBoardWithNothing(world);
        drawWorld(world, 3, 3);

        ter.renderFrame(world);
    }
}
```

