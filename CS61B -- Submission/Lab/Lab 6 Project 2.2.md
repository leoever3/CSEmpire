### Abstraction

Interactivity



#### Memory Game

1. Create the game window
2. Randomly generate a target string
3. Display target string on screen one character at a time
4. Wait for player input until they type in as many characters as there are in the target
5. Repeat from step 2 if player input matches the target string except with a longer random target string. If no match, print a game over message and exit.

### What to do

###### generateRandomString

String -- Char

* "B" -- 'B'

* `String B = Character.toString('B');`

```java
 public String generateRandomString(int n) {
        //TODO: Generate random string of letters of length n
        String res = new String();
        for (int i = 0; i < n; i += 1) {
            int k = uniform(rand, CHARACTERS.length - 1);
            res += CHARACTERS[k];
        }
        return res;
    }
```



###### drawFrame

1. Clears the canvas
2. sets the font to be large and bold (size 30)
3. Draws the input string centered on the canvas
4. shows the canvas on the screen

```java
    public void drawFrame(String s) {
        //TODO: Take the string and display it in the center of the screen
        //TODO: If game is not over, display relevant game information at the top of the screen
        int midWidth = width / 2;
        int midHeight = height / 2;

        StdDraw.clear();
        StdDraw.clear(Color.black);

        // Draw the actual text
        Font bigFont = new Font("Monaco", Font.BOLD, 30);
        StdDraw.setFont(bigFont);
        StdDraw.setPenColor(Color.RED);
        StdDraw.text(midWidth, midHeight, s);
        StdDraw.show();
    }
```

###### flashSequence

* one letter a time

```java
public void flashSequence(String letters) {
        //TODO: Display each character in letters, making sure to blank the screen between letters
        for (int i = 0; i < letters.length(); i++) {
            drawFrame(letters.substring(i, i + 1));
            StdDraw.pause(750);
            drawFrame(" ");
            StdDraw.pause(750);
        }
    }
```

###### solicitNCharsInput

* Draw the letters typed by player

```java
public String solicitNCharsInput(int n) {
    //TODO: Read n letters of player input
    String input = "";
    drawFrame(input);

    while (input.length() < n) {
        if (!StdDraw.hasNextKeyTyped()) {
            continue;
        }
        char key = StdDraw.nextKeyTyped();
        input += String.valueOf(key);
        drawFrame(input);
    }
    StdDraw.pause(500);
    return input;
}
```

###### startGame

```java
public void startGame() {
    //TODO: Set any relevant variables before the game starts
    gameOver = false;
    playerTurn = false;
    round = 1;

    //TODO: Establish Game loop
    while (!gameOver) {
        playerTurn = false;
        drawFrame("Round " + round + "! Good luck!");
        StdDraw.pause(1500);


        String roundString = generateRandomString(round);
        flashSequence(roundString);

        playerTurn = true;
        // not come out of the loop in solicitNCharsInput until player
        // inputs enough characters
        String userInput = solicitNCharsInput(round);

        if (!userInput.equals(roundString)) {
            gameOver = true;
            drawFrame("Game Over! Final level: " + round);
        } else {
            drawFrame("Correct, well done!");
            StdDraw.pause(1500);
            round += 1;
        }
    }

}
```

###### Helpful UI

```java
// Draw the GUI
if (!gameOver) {
    Font smallFont = new Font("Monaco", Font.BOLD, 20);
    StdDraw.setFont(smallFont);
    StdDraw.textLeft(1, height - 1, "Round: " + round);
    StdDraw.text(midWidth, height - 1, playerTurn ? "Type!" : "Watch!");
    StdDraw.textRight(width - 1, height - 1, ENCOURAGEMENT[round % ENCOURAGEMENT.length]);
    StdDraw.line(0, height - 2, width, height - 2);
}
```





#### Programming Paradigms

* Good coding practice is to first build small procedures with explicit purposes and then compose more complex methods using the basic ones
* identifying the steps of your game and breaking it apart into individual methods