### Lab 5: Getting Started on Project 2

##### Part 1 Meet the Tile Rending Engine

<u>BoringWorldDemo.java</u>

* Initializing the tile rendering engine
* Generating a two dimensional Tetile[] [] array.
* Using the tile rendering engine to display the Tetile[] [] array



**API (application programming interface)**

###### Boring World

1. Creating **TERenderer** object

   Initialize

​		Pixel 像素 16 * 16

2. **Tetile** objects 
   1. TETile constructer -- TETile.java
   2. Tileset.java
      1. WALL
      2. FLOWER ...
3. Draw



###### Ramdom World

* **Radom class** -- pseudorandom numbers 伪随机数
  * get different sequences by choosing seed

* **Switch**
* **Delegates** work to functions with clearly defined behavior



##### Part 2: Use the Tile Rendering Engine

* Define private helper method

###### Hint

public static void addHexagon(TETile[][] world, Position p, int s, TETile t), where Position is a very simple class with two variables p.x and p.y and no methods. p specifies the lower left corner of the hexagon.



First: I wrote a couple of methods that compute the bottom-left Position of a current hexagon’s neighbors. For example, I wrote topRightNeighbor, which computed the right thing to pass to addHexagon so that I could get my topRight neighbor. I did not write JUnit tests for this because I knew it’d be easy to visually test, though JUnit tests would have been fine. I then wrote bottomRight, and ended up with 3 whole hexagons out of the 19 I wanted.

Second: I tried to figure out how I could use bottomRight and topRight in some clever way to get the whole grid, but was a bit stymied. I considered trying to use recursion in some way, but it didn’t feel like the right solution for symmetry reasons (too much weird backtracking). I then thought about whether I’d be stuck having to write six different neighbor methods, and decided that seemed excessive. All of this was done without any coding. If I’d have started coding all this, it would have been a huge waste of time.”

Third: Stepping back, I decided to try to find the “nicest” way to try to lay out my hexagons and was ready to throw away my bottomRight and topRight methods entirely. Then the key AHA moment occurred when I noticed that the world consists of 5 columns of 3, 4, 5, 4, and 3 hexagons, respectively.

Fourth: I wrote a method called drawRandomVerticalHexes that draws a column of N hexes, each one with a random biome.

Fifth: I wrote a main method that is a little ugly, but basically calls drawRandomVerticalHexes five times, one for each of the five columns of the world, consisting of 3, 4, 5, 4, and 3 hexagons. To figure out the starting position for the “top” hex of each column, I used the topRightNeighbor or bottomRightNeighbor on the old top, as appropriate.

Sixth: I added some code to allow for interactivity so you can press a single key to get a new random world and enjoyed playing around with it. But interactivity will have to wait until next week’s lab for you guys.