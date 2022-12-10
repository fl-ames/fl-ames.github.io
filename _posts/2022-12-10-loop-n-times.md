---
title: Loop n Times
subtitle: How to repeat a specific section of your flow a fixed number of times
layout: post
---

The technique I am about to describe is not particularly advanced. Anyone could easily come up with it on their own. However, this is a good starting point for me to see how I will approach these topics in my blog, and for you to gain an understanding of what this blog is trying to accomplish. Having said that, let me explain how I encountered this challenge.

The first game I made using Flow Builder was Nim. If you're not familiar with it, Nim is a simple game where players take turns removing objects from a pile until there are none left. The player who empties the pile loses the game.

When I was developing this game, I had the idea of creating a series of Christmas-themed games. I chose to use the emojis 🎄 and 🌲 to represent the pile in the Nim game. The player and the computer will take turns transforming the pine trees into Christmas trees. The player who lights up the last Christmas tree loses the game.

## Approach

I want to display a line of tree emojis that can be in a decorated or undecorated state, like this:
```
🌲🌲🌲🌲🌲🌲🌲
'''
or 
'''
🎄🎄🎄🌲🌲🌲🌲
'''
One approach could have been to create a separate text variable for each possible line, but this would require a large number of variables and would make the flow more complex when it came time to display the text. Additionally, if the size of the pile changed, the entire game would have to be rebuilt. Therefore, I needed to come up with a solution that could dynamically generate the text variable using logic. 

To break the development process into manageable chunks, the first step I took was to dynamically generate a line of emojis of a certain length.

I created a text variable to hold the emoji's
- Create a New Resource
- Resource Type: **Variable**
- API Name: **varTextTreeDisplay**
- Description: **Textual representation of the state of game**
- Data Type: **Text**
- Leave the rest untouched and click **Done**


