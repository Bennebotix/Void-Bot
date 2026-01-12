### Void-Bot
A minimax bot for all 2-player turnbased games (Chess, TicTacToe, etc...)

## Installation

Just load `void_bot.min.js` into your project before all of your assets:
```HTML
<script type="text/javascript" src=""></script>
```

## Usage

```JavaScript
const bot = new Bot(
  "X" /* id used for the player, can be anything */,


  ( /*
      score function that calculates the score of a player at a certian game state
      negative values are sates the bot wants to avoid
    */
    gameState /* the current sate (like JSON object, array, etc...) */,
    player /* player id */
  ) => {
    /* v example v */
    let win = window.hasPlayerWon(player, gameState);
    let loss = window.hasPlayerLost(player, gameState);
    let tie = window.hasPlayerTied(player, gameState);
    /* ^ example ^ */

    if (win) {
      return { state: "finalized", value: 10, name: "win" }; /* value can be anything, but this is how you return a win */
    } else if (loss) {
      return { state: "finalized", value: -10, name: "loss" }; /* same here */
    } else if (tie) {
      return { state: "finalized", value: -3, name: "tie" }; /* same here */
    }

    return { state: "stillGoing", value: 0, name: "none" }; /* th game hasn't ended yet */
  },


  ( /* possible moves funcion */
    gameState,
    player
  ) => {
    /* v example v */
    return window.possibleMovesForPlayer(player, gameState);
    /* ^ example ^ */
  },


  ( /* play function, makes a move */
    moveId
    /*  the id for the move that needs to be played, examples:
          Tic Tac Toe: "X5" for player X going in the middle square
          Chess: "e4 e5" ofr the piece in spot e4 moves to e5
    */
  ) => {
    /* v example v */
    window.makeMove(moveId);
    window.drawGame();
    /* ^ example ^ */
  },


  ( /* simulated game state function, simulaes moves on the board */
    gameState,
    moves /* a list of move ids */
  ) => {
    /* v example v */
    let newGameState = [...gameState];
    moves.forEach((move) => {
      // Change newGameState to simulate move
    });
    return newGameState;
    /* ^ example ^ */
  },


  (
    /* game state function, should return the current gamestate */
  ) => {
    /* v example v */
    return window.getCurrentGameState();
    /* ^ example ^ */
  },

  ( /* can block functon, return wether a certain move can be blocked */
    gameState,
    player, /* the player to de the blocking */
    move /* the move id to be blocked */
  ) => {
    /* v example v */
    return true; /* example for tic tac toe, because every move can be blocked */
    /* ^ example ^ */
  },


  10 /* maxumim depth for the bot to search */
);

// To make a move, run "bot.move()"
```
