### Void-Bot

## Usage

```JavaScript
class Bot{constructor(b,f,g,e,c,k,l){this.pI=b;this.sF=f;this.gMF=g;this.pF=e;this.stF=c;this.gSF=k;this.mD=l;this.s=class{constructor(d,a,m,n){this.id=d;this.d=a;this.p=n;this.gS=this.p.stF(m,[this.id]);this.o=this.p.sF(this.gS,this.p.pI);this.mover=(this.p.pI+(this.d-1)%2-1)%2+1;this.c=[];this.b="finalized"==this.o.state;!this.b&&this.d<this.p.mD&&this.fill()}fill(){let d=this.p.gMF(this.gS,this.mover%2+1);for(let a=0;a<d.length;a++)this.c.push(new this.p.s(d[a],this.d+1,this.gS,this.p))}get s(){let d=this.c.some(a=>"loss"==a.o.name);return 1==this.d&&d?-Infinity:this.b?this.o.value/Math.pow(this.d,2):this.c.map(a=>a.s).reduce((a,h)=>a+h,0)}}}get gS(){return this.gSF()}play(){let b=this.gMF(this.gS,this.pI),f=-Infinity,g={id:b[b.length-1]};for(let e=0;e<b.length;e++){let c=new this.s(b[e],1,this.gS,this);c.s>f&&(g=c,f=c.s)}this.pF(g.id)}};

const bot = new Bot(
  "X" /* id used for the player, can be anything */,


  ( /*
      score function that calculates the score of a player at a cartian game state
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
    gameState /* the current sate (like JSON object, array, etc...) */,
    player /* player id */
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
    moves
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


  10 /* maxumim depth for the bot to search, this get pretty bi pretty fast */
);

// To make a move, run "bot.play()"
```
