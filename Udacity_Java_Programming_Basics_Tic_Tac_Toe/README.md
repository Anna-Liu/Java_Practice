# Udacity's Java Programming Basics: Tic Tac Toe Exercise

Code for checking for a winner. I only added code/modified the Game.java file. The GameUI.java file is included to understand the code.

My addition:
```
public String checkGameWinner(char[][] grid) {
        String result = "None";

        if (freeSpots <= 4) { //only checks for a winner if there are at least 5 plays on the grid
            if (grid[0][0] == turn && (grid[0][0] == grid[1][1] && grid[1][1] == grid[2][2])) { //checks downwards diagonal
                result = Character.toUpperCase(turn) + " wins";
                return result; //exits method without checking the other statements
            }
            if (grid[0][2] == turn && (grid[0][2] == grid[1][1] && grid[1][1] == grid[2][0])) { //checks upwards diagonal
                result = Character.toUpperCase(turn) + " wins";
                return result;
            }
            for (int i = 0; i < 3; i++) {
                int counterHorizontal = 0; //counts the number of the turn's (X or O) symbols in the same horizontal row. Reset to 0 when a new row is reached
                int counterVertical = 0; //counts the number of the turn's (X or O) symbols in the same vertical column. Reset to 0 when a new column is reached
                for (int j = 0; j < 3; j++) {
                    if (turn == grid[i][j]) { //checks vertical line
                        counterVertical++;
                    }
                    if (turn == grid[j][i]) { //checks horizontal line
                        counterHorizontal++;
                    }
                    if (counterHorizontal == 3 || counterVertical == 3) {
                        result = Character.toUpperCase(turn) + " wins";
                        return result;
                    }
                }
            }
            if (freeSpots == 0) { //Tie if all the other conditions are false and there are no more free spots
                result = "Tie";
            }
        }
        return result;
    }

```

Added changing of turns for non two-player game:
```
public void nextTurn() {
        //check if single player game, then let computer play turn
        if (!twoPlayer) {
            if (freeSpots == 0) {
                return; //bail out if no more free spots
            }
            int ai_i, ai_j;
            do {
                //randomly pick a position (ai_i,ai_j)
                ai_i = (int) (Math.random() * 3);
                ai_j = (int) (Math.random() * 3);
            } while (grid[ai_i][ai_j] != '-'); //keep trying if this spot was taken
            //update grid with new play, computer is always o
            turn='o'; //switch to computer
            grid[ai_i][ai_j] = 'o';
            //update free spots
            freeSpots--;
            doChecks();
            turn='x'; //switch to player
        } else {
            //change turns
            if (turn == 'x') {
                turn = 'o';
            } else {
                turn = 'x';
            }
        }
        return;
    }
```
