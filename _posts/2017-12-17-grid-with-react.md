---
layout: post
title:  "A Board with React"
description: "Drawing the game board for the Game of Life."
date:   2017-12-17 16:15:00 +0000

---

I previously showed a working [timer](https://ashlynnpai.github.io/journal/timer-with-react/) that would form the backbone of my Game of Life population simulation, by updating the population and the game board on each tick. With the timer working I started on the game board.

### Design Choices

I had a few obvious choices to make when deciding how to make the game board. I knew I wanted to make a square board and I thought a 1d array would work well. I filled the array with either "X" or "O" representing alive or dead so it would be easy to see what was going on. I gave the board a small seed of X's to start with. All those X's and O's will be hidden from the board when it is drawn. If a square is alive, the color will change. That gets handled in the render function, which will set the color of each square.

#### Game Board with React.js

~~~ javascript

class Game extends React.Component {
    constructor(props) {
        super(props);
        this.size = 4900;
        let initialSquares = Array(this.size).fill("O");
        let seed = [775, 776, 777, 845, 916];
        for (let i=0; i<seed.length; i++) {
            initialSquares[seed[i]]="X";
        }
        this.state = {
            squares: initialSquares,
        };
    }
    
~~~
~~~
  
    render() {
        return (
            <div id="board" className="flex-container">
                {this.state.squares.map((square,index) => 
                <div className={square + "color"}  id={"square" + index} key={index}></div>)}
            </div>
        );
    }
}

ReactDOM.render(
    <Game />,
    document.getElementById('app')
);
~~~

#### SCSS

The SCSS is where I control the layout of the board. I used Flexbox to let the elements wrap to the next line when they had filled up the available space.

~~~ scss

$font-stack: Roboto;
$board-color: #4b535c;
  
body {
  text-align: center;
  font-family: $font-stack;
}

.flex-container {
  display: flex;
  justify-content: center;
  background-color: #4b535c;
  flex-direction: row;
  flex-wrap: wrap;
  max-width: 850px;
  margin: 0 auto;
}

.flex-container>div {
  width: 10px;
  height: 10px;
  border: solid 1px #505963;
  text-align: center;
}

.Xcolor {
  background: #E55EA2;
}

.Ocolor {
  background: $board-color;
}

~~~

Here is what the board looks like once the population gets going:

<img alt="Game of Life with React" src="https://www.ashlynnpai.com/assets/lifesim.gif" width="400" />

And here is the [code](https://codepen.io/ashlynnpai/pen/qVeWdJ) for the complete simulation.