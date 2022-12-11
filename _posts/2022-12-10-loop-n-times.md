---
title: Loop n Times
subtitle: How to repeat a specific section of your flow a fixed number of times
layout: post
---

The main focus of this article is to demonstrate how to repeat a section of your flow a specific number of times. You might think that you need to use the loop element for this, but that is not the case. A loop element is used to iterate over a collection of items and perform an action on each element in the collection. When you simply want to repeat a certain part of your flow a certain number of times, you need to construct the loop yourself.

The technique I am about to describe is not particularly advanced. Anyone could easily come up with it on their own. However, this is a good starting point for me to see how I will approach these topics in my blog, and for you to gain an understanding of what this blog is trying to accomplish. Having said that, let me explain how I encountered this challenge.

## A Christmas-themed game

The first game I made using Flow Builder was [Nim](https://en.wikipedia.org/wiki/Nim). If you're not familiar with it, Nim is a simple game where players take turns removing objects from a pile until there are none left. The player who empties the pile loses the game.

When I was developing this game, I had the idea of creating a series of Christmas-themed games. For this Christmas variant of Nim the player and the computer take turns decorating Christmas trees and who lights up the last Christmas tree loses the game.

This is a recording of me playing the game:
![Nim gameplay](/assets/img/nimgameplay.gif){: .mx-auto.d-block :}

I chose to use the emojis 🎄 and 🌲 to represent the pile of the Nim game. The state of the game is represented by a line of tree emojis that are either decorated or undecorated.

## Displaying a line of Christmas trees

One approach could have been to create a separate text variable for each possible state of the trees (no decorated tree, one decorated tree, two decorated trees etc...). This would require a large number of variables and would add to the complexity of the flow when it came to displaying the right text variable. Additionally, if the size of the pile changed, the entire game would have to be rebuilt. I needed to come up with a solution that could dynamically generate the text variable using logic.

To break the development process into manageable chunks, the first step I took was to dynamically generate a line of emojis of a certain length.

Let's create an empty text variable to hold the emojis:

- Resource Type: **Variable**
- API Name: **TreeDisplay**
- Data Type: **Text**
  
To determine the number of emojis to be displayed, create another variable. This variable will store the total number of trees in the game. (In this case I gave it a default value of 21)

- Resource Type: **Variable**
- API Name: **TreeTotal**
- Data Type: **Number**
- Decimal Places: **0**
- Default Value: **21**

And then the most important action in this setup: let's add an **Assignment** element to the flow to add an emoji to the empty varTextTreeDisplay variable:
- Label: **Add one emoji to TreeDisplay**
- API Name: **Add_one_emoji_to_TreeDisplay**
- Variable: **{!TreeDisplay}**
- Operator: **Add**
- Value: **🌲**

The assignment element we just created is the section that we want to repeat. If we can repeat this element 21 times, we will end up with our first goal, a text variable containing 21 tree emojis.

## Constructing the loop

A loop must have a condition that determines when it should stop running. If a loop continues indefinitely, it will consume all of the available memory resources. In our case if a flow exceeds the maximum number of elements allowed (which is 2000), it will give an error. 


## Professional use

Never will there be a usecase that needs a solution with Christmas trees 

🟢🟢🟢🟢🟢🟢⚪⚪⚪⚪ 6/10

