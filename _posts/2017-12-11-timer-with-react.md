---
layout: post
title:  "A Timer with React"
description: "Make a simple countdown timer with React.js."
date:   2017-12-11 14:00:00 +0000

---

I made a population simulation based on Conway's Game of Life using React. The [simulation](https://codepen.io/ashlynnpai/pen/qVeWdJ) updates the state of the population with each tick. This is the skeleton code for a timer which can be used to make projects that update at a timed interval. I wanted to show the code for the timer separately so it would be easier to read.

#### Timer with React.js

~~~ javascript

class Timer extends React.Component {
    constructor(props) {
        super(props);
        this.state = {count: 10};
    }

    componentDidMount() {
        this.timerID = setInterval(
            () => this.tick(),
            1000
        );
    }
  
    doSomething() {
        if (this.state.count == 0) {
            clearInterval(this.timerID);
        }
    }

    tick() {
        this.setState({
            count: this.state.count - 1
        });
        this.doSomething();
    }
    
~~~
~~~

    render() {
        return (
            <div>
                <h1>{this.state.count}</h1>
            </div>
        );
    }
}

ReactDOM.render(
    <Timer />,
    document.getElementById('app')
);

~~~

This example displays a timer that counts down from ten and stops at zero. The doSomething function fires at each interval. I'll be using this function to update the population state later.