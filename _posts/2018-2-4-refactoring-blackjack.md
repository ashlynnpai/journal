---
layout: post
title:  "A Little RPG Dungeon Crawler"
description: "Making my first RPG game with React."
date:   2018-2-4 4:10:00 +0000

---

I was doing some spring cleaning on my Github repositories and found an old text-based blackjack game that was kind of a mess. Aside from some things that definitely needed fixing like variables that were declared and left unused, the game was originally written as player vs. dealer. Both the classes and the methods had been written to not accommodate any more computer players. My cleanup focused on rewriting the game to add more computer opponents.

Since the player, dealer and other computer opponents would share the same attributes, I created a Participant class to initialize the attributes and had the other classes inherit from it. The player class was the only one that was human controlled. The dealer class differed from the other computer opponents in a couple of ways. First, the dealer has to show one card during the first round, whereas the other computer opponents keep theirs hidden. Second, the dealer goes last. The dealer is also required to hit until 17, whereas the other opponents are not, but I didn't think writing different algorithms for that was too exciting, so I made all the computer-controlled participants follow the same rule.

Then I had to fix the methods which were previously using variables to store the player and dealer scores, and rewrote them to keep track of all scores in a hash, and store the winners in an array since there are likely to be multiple winners in each round.

I also added tests to verify that multiple aces were being computed correctly. This had nothing to do with adding more opponents but I was concerned about the edge cases being handled properly. The game creates a deck of cards that are dealt out and computes the value of the cards in each hand. Instead of generating a full deck during the test, I wrote a method that just stubbed out the deck with the cards I wanted evaluated.

Here is the repository: https://github.com/ashlynnpai/blackjack