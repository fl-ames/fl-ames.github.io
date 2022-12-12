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

The first step I took was to dynamically generate a line of emojis of a certain length.

I created an empty text variable to hold the emojis:

- Resource Type: **Variable**
- API Name: **TreeDisplay**
- Data Type: **Text**
  
To determine the number of emojis to be displayed, I created another variable. This variable stores the total number of trees in the game. (In this case I gave it a default value of 21)

- Resource Type: **Variable**
- API Name: **TreeTotal**
- Data Type: **Number**
- Decimal Places: **0**
- Default Value: **21**

And then the most important action in this setup: I added an **Assignment** element to the flow to add an emoji to the empty varTextTreeDisplay variable:
- Label: **Add one emoji to TreeDisplay**
- API Name: **Add_one_emoji_to_TreeDisplay**
- Variable: **{!TreeDisplay}**
- Operator: **Add**
- Value: **🌲**

The assignment element is the section that we want to repeat. If we can repeat this element 21 times, and add the tree emoji every time, we will end up with our first goal, a text variable containing 21 tree emojis.

## Constructing the loop

A loop must have a condition that determines when it should stop running. If a loop continues indefinitely, it will consume all of the available memory resources. In case of Salesforce there is limit of allowed elements to call in a flow (which is 2000). If a loop does not stop and you reach the 2000 elements, your flow will break and an error will be given. 

To determine if the loop should stop running I added a decision element before the assignment element:
- Label: **Are all trees on display?**
- API Name: **Are_all_trees_on_display**
  - Outcome Label: **Yes all on display**
  - Outcome API Name: **Yes all on display**
  - Condition Requirements to Execute Outcome: **All Conditions Are Met (AND)**
  - Resource: **{!TreeTotal}**
  - Operator: **Equals**
  - Value: **0**

So the decision checks if the TreeTotal variable is equal to zero to leave the loop.

I replaced the assignment element in the flow to the default outcome of the decision and I added another assignment to the assigment element:

- Variable: **{!TreeTotal}**
- Operator: **Subtract**
- Value: **1**


In the assignment element we already implemented in the flow I added an extra assignment:
- Variable: TreeTotal
- Operator: Subtract
- Value: 1

then I created a path from the assignment element back to the decision element

At last I added a screen element on the 'Yes all on display' path of the decision. It's just a screen with a display text component on it with the resource **{!TreeDisplay}** as a value.

Here is what the flow looks like now:

IMG OF FLOW

So what is happening here?
Blablabla

I could have added the decision element after the assignment and make the loop work perfectly fine for this case. The only difference in placing the decision before the section you want to repeat is that the loop condition is always checked, if you place it after the section, the section will always run at least once.



## Professional use

Although the looping technique can be universally applied, the full technique described can be used in a variety of situations:
In a relation to games, what do you think about creating a health bar like this: 🧡🧡🧡🤍🤍 ?

And in professional use I can imagine a rating bar created with exact the same technique like this: 🟢🟢🟢🟢🟢🟢⚪⚪⚪⚪ 6/10

