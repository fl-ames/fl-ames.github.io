---
title: Loop n Times
subtitle: How to repeat a specific section of your flow a fixed number of times
layout: post
---

The technique I am about to describe is not particularly advanced. Anyone could easily come up with it on their own. However, this is a good starting point for me to see how I will approach these topics in my blog, and for you to gain an understanding of what this blog is trying to accomplish. Having said that, let me explain how I encountered this challenge.

The first game I made using Flow Builder was [Nim](https://en.wikipedia.org/wiki/Nim). If you're not familiar with it, Nim is a simple game where players take turns removing objects from a pile until there are none left. The player who empties the pile loses the game.

When I was developing this game, I had the idea of creating a series of Christmas-themed games. The player and the computer will take turns decorating Christmas trees. The player who lights up the last Christmas tree loses the game. I chose to use the emojis 🎄 and 🌲 to represent the pile in the Nim game. The state of the game is represented by a line of tree emojis that are either decorated or undecorated, like this: 🎄🎄🎄🌲🌲🌲🌲

## Create a line of trees

One approach could have been to create a separate text variable for each possible line of tree emojis, but this would require a large number of variables and would make the flow more complex when it comes to displaying the text. Additionally, if the size of the pile changed, the entire game would have to be rebuilt. Therefore I needed to come up with a solution that could dynamically generate the text variable using logic.

To break the development process into manageable chunks, the first step I took was to dynamically generate a line of emojis of a certain length.

I created an empty text variable to hold the emojis:

- Resource Type: **Variable**
- API Name: **TreeDisplay**
- Data Type: **Text**
  
To determine the number of emojis to be displayed, I created another variable. This variable will store the total number of trees in the game. (In this case I gave it a default value of 21)

- Resource Type: **Variable**
- API Name: **TreeTotal**
- Data Type: **Number**
- Decimal Places: **0**
- Default Value: **21**

Let's add an **Assignment** element to the flow to add a tree to the empty varTextTreeDisplay variable:
- Label: **Add one emoji to TreeDisplay**
- API Name: **Add_one_emoji_to_TreeDisplay**
- Variable: **{!TreeDisplay}**
- Operator: **Add**
- Value: **🌲**

The main focus of this article is to demonstrate how to repeat a section of your flow a specific number of times. The assignment element we just created is the section that we want to repeat.  If we can repeat this element 21 times, we will end up with a text variable containing 21 emojis. 
You might think that you need to use the loop element for this, but that is not the case. A loop element is used to iterate over a collection of items and perform an action on each element in the collection. When you simply want to repeat a certain part of your flow a certain number of times, you need to construct the loop yourself.

### Constructing the loop

A loop must have a condition that determines when it should stop running. If a loop continues indefinitely, it will consume all of the available memory resources. If a flow exceeds the maximum number of elements allowed (which is 2000), it will give an error.




