**If I plan to rebuild this huge project someday in the future, Go to the Summary part directly !**



### Pre-lab

* Lab 5
  * Draw the world
  * Ramdom
* Lab 6
  * UI
  * Display



### Abstraction

* Build a 2-D tile based game
* Provided -- rendering engine 渲染引擎
  * Need not think of individual pixels
* Some elements
  * Treasures
  * Animals
  * Locked doors

### Tips

* Complexity should arise through easy to understand interactions between simple components.
* Rebuild
* Refactor
* Do not share state between methods.
  * Deep misery
  * Debug hell
* Instead, methods should do very clear things and ideally talk exclusively with other methods using return values and parameters.
* Return multiple things -- make a class
  * Position (int x, int y)



### Skeleton Code Structure

* `Byog.TileEngine`
  * TERenderer.java: rendering
  * TETile: draw a single tile
  * Tileset: tiles library (flowers, grasses...)
* `Byog.Core`
  * RandomUtils.java
  * Main.java -- the door
  * Game.java -- the entry hall
  * More



### Phase 1: Worrld Generation

* Pseudorandomly generated
* map
  * rooms
  * hallways
  * outdoor spaces
* All values should be non-null, i.e. make sure to fill them all in before calling `renderFrame`.
* Add your own tiles in Tileset.java





![image-20220128132412769](/Users/morningstar/Library/Application Support/typora-user-images/image-20220128132412769.png)





```java
package byog.Core;

import byog.TileEngine.TERenderer;
import byog.TileEngine.TETile;
import byog.TileEngine.Tileset;

import java.util.Random;

import static byog.Core.RandomUtils.uniform;

public class MapGenerator {
    private static final int WIDTH = 80;
    private static final int HEIGHT = 30;
    private static final long SEED = 123723;
    private static final Random RANDOM = new Random(SEED);

    /**
     * Constructor
     */
    public MapGenerator(int width, int height) {

    }

    public static void main(String[] args) {
        MapGenerator g = new MapGenerator();
        g.generator();
    }

    /**
     * Generate the map
     */
    public static void generator() {
        // initialize the tile rendering engine with a window of size WIDTH x HEIGHT
        TERenderer ter = new TERenderer();
        ter.initialize(WIDTH, HEIGHT);

        // initialize tiles
        TETile[][] tiles = new TETile[WIDTH][HEIGHT];
        fillTilesWithNothing(tiles);

        // draw random rooms
        int roomNum = uniform(RANDOM, 23, 25);
        Room[] rooms = Room.drawRanRooms(tiles, roomNum, RANDOM);

        // sort rooms by X axis
        rooms = Room.sortRoomsByX(rooms);
        // draw hallways between each rooms
        for (int i = 0; i < rooms.length - 1; i += 1) {
            Position p1 = rooms[i].ranTileInside(RANDOM);
            Position p2 = rooms[i + 1].ranTileInside(RANDOM);
            Hallway.drawHallway(tiles, p1, p2);
        }


        // draws the world to the screen
        ter.renderFrame(tiles);

    }

    /**
     * fill all the tiles with nothing to initialize tiles
     */
    public static void fillTilesWithNothing(TETile[][] tiles) {
        int height = tiles[0].length;
        int width = tiles.length;
        for (int x = 0; x < width; x += 1) {
            for (int y = 0; y < height; y += 1) {
                tiles[x][y] = Tileset.NOTHING;
            }
        }
    }
}

```



###### Unsolved bug

```
                                              ######                            
                                              #····#               #####        
             ######                           #····#               #···#        
             #····# ######                    #····#               #···#        
   #####     #····# #····#                    #····#               #···#        
   #···#     #····# #····#                    ##·###        ###### #···#        
   #···#     #····# #····#         ########### #·#          #····# #···#        
   #···#     #··### #····#         #··##·····# #·#          #····# ##·##        
   #··##     #··#   ##·########    #··##·····# #·#          #·####  #·#         
   #··#      #··#    #·# #····#    #··##·····# #·#          #·#     #·#         
   #··#      #··#    #·# #····#    #··##·····# #·#          #·#     #·#         
   #··#      #··#    #·# #····#    #··##·····# #·#          #·#     #·#         
   #··#      #··#    #·# #····#    #·###·##·####·#     ######·#     #·#         
   #··#      #··#    #·# #····#    #·#···##····#·#######······#     #·#         
 ###··##     #··######·# ###·##    #·····##····#··············#     #·#         
 #·····#     #······##·#   #·#     #·#·#·###·###·#######······#     #·#         
 #·····#     #·········#   #·#     #·····# #·# #·#     #······#     #·####      
 #·····#     ##·####█#·#   #·#     #·····# #·# #·#     #····@·#     #····#      
 #·····#    ###·##   #·#   #·#     #·····# #·###·####  ######·#     #····#      
 ####·#######····#   #·#   #·#     #·#·### #·##·····#       #·#     #·#·##      
    #············#   #·# ###·#######·#·#####········#       #·#     #·#·#       
    ##############   #·###···#·····#·#····#####·····#       #·# #####·#·######  
                     #·······#·····#·#····#   #######       #·###·····#·#····#  
                     #####·········#·#····#                 #·········#·#····#  
                         #####·······######                 ###########······#  
                             #########                                ########  

```

```
                                                                              
                                              ######                            
                                              #····#               #####        
             ######                           #····#               #···#        
             #····# ######                    #····#               #···#        
   #####     #····# #····#                    #····#               #···#        
   #···#     #····# #····#                    ##·###        ###### #···#        
   #···#     #····# #····#         ########### #·#          #····# #···#        
   #···#     #··### #····#         #··##·····# #·#          #····# ##·##        
   #··##     #··#   ##·########    #··##·····# #·#          #·####  #·#         
   #··#      #··#    #·# #····#    #··##·····# #·#          #·#     #·#         
   #··#      #··#    #·# #····#    #··##·····# #·#          #·#     #·#         
   #··#      #··#    #·# #····#    #··##·····# #·#          #·#     #·#         
   #··#      #··#    #·# #····#    #·###·##·####·#     ######·#     #·#         
   #··#      #··#    #·# #····#    #·#···##····#·#######······#     #·#         
 ###··##     #··######·# ###·##    #·····##····#··············#     #·#         
 #·····#     #······##·#   #·#     #·#·#·###·###·#######······#     #·#         
 #·····#     #·········#   #·#     #·····# #·# #·#     #······#     #·####      
 #·····#     ##·####█#·#   #·#     #·····# #·# #·#     #····@·#     #····#      
 #·····#    ###·##   #·#   #·#     #·····# #·###·####  ######·#     #····#      
 ####·#######····#   #·#   #·#     #·#·### #·##·····#       #·#     #·#·##      
    #············#   #·# ###·#######·#·#####········#       #·#     #·#·#       
    ##############   #·###···#·····#·#····#####·····#       #·# #####·#·######  
                     #·······#·····#·#····#   #######       #·###·····#·#····#  
                     #####·········#·#····#                 #·········#·#····#  
                         #####·······######                 ###########······#  
                             #########                                ########  

```



### Summary

#### What we have done

##### Phase 1

1. Draw random room in tiles
2. Draw random hallway to connect all the rooms
3. Draw the user and player
4. Generate the maze

###### Files

1. Position.java
2. Room.java
3. Hallway.java
4. MapGenerator.java -- Main file in phase 1

###### Not finished

1. Add one more Tileset (like golden to get score)
2. Add more mechanism like shadow the unexplored zone
3. Give the user more option to the player he would like to control



##### Phase 2

1. Generate the map by user
2. Generate the map by the input String
3. the player could control the player to move around and leave the maze
4. Enable the player could save and load the game (serializable)



###### Files

1. GameUI.jav
   1. Draw the initial menu and do the Control parts. 
   2. It's kind of belonging to the Game.kava
