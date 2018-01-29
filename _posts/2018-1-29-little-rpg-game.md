---
layout: post
title:  "A Little RPG Dungeon Crawler"
description: "Making my first RPG game with React."
date:   2018-1-29 19:20:00 +0000

---

I made my first RPG dungeon crawler game using React.js as part of the Data Visualization program at FreeCodeCamp. I probably wouldn't have made one otherwise, but it turned out to be my favorite project. React made it easy to create combat logs and health bars that needed almost continuous, fast updating.

<img src="https://www.ashlynnpai.com/assets/level1-700-min.png" width="600" alt="Silverheart RPG" class="img-center" />

### Game Design

At first I wanted to pile all kinds of features into the game but after spending over a month on it I decided to wrap it up and go with what I had. It has three levels and a boss fight, quests, magic items (weapons, armor and quest items) that give bonuses, and a pet.

I definitely wanted interactive combat so I used timers to manage the flow of combat. I wanted the player to defeat ordinary enemies ("mobs") quickly so they don't get bored but I wanted the boss fight to require using a variety of skills as well as potions. To do this I made the damage quite high on a skill called Fury but put it on a cooldown timer so it couldn't just be spammed. That way on the boss fight the boss would have time to use his own skills.

If the player dies fighting the boss, which they very well might, not to fear, they will be offered the chance to be revived by the pet cat that lives there, whether or not they have acquired the cat as a pet. They'll be given a full set of health and mana potions if they die during the boss fight.

Originally I wanted to track the casting time for skills and make them interruptable. However, when I played through the boss fight I felt there was already enough going on. Instead I just went with what I had already given to the ordinary mobs, a skill that continuously did damage on the player until it was actively removed and instead of having it only cast one time, the boss will continually cycle through the different skills. I tried to tune the fight so that if the player never removes the curse, they can't win the fight. However, it should be fine to miss sometimes if they also heal themselves and use their potions. 

I think my biggest mistake was that my original concept of the map really didn't work. I had the full map displaying all the time with the browser supposedly tracking the position using window.scrollTo(x-coord, y-coord). I had everything split up into rooms and putting a certain number of mobs in each room. However I didn't have enough tiles in each row and despite being in separate rooms they still all looked clumped together, which made the rooms mostly pointless. Then when I tested at different resolutions I realized the game was unplayable on small screens with the large UI I had created surrounding the map. So after I was almost done with the game I ended up overhauling the map, getting rid of rooms (which worked out well because the game art tiles I chose fit better with a grand hall concept anyway), shrinking the tiles and breaking them into three levels with staircases separating them. The game should now be comfortable to play on browser resolution height of at least 768px. 

One disappointment was that I wanted to use a running sprite but couldn't find one that fit my game. I did spend countless hours trying to find game art. The sites opengameart.com and soundbible.com were very helpful.

This was my first RPG game, so if you have any feedback for me, please let me know. Also, my knowledge of React.js is just from reading lots of blog posts, the official documentation and one book, Learning React: Functional Web Development with React and Redux.

The game is hosted at Codepen: <https://codepen.io/ashlynnpai/full/ZvwZmQ/>

Currently all the Javascript is in one file in my Github, since it all needed to be in one file to be hosted at Codepen.  I'll refactor it at a later date.

<https://github.com/ashlynnpai/dungeon/blob/master/script.js>




