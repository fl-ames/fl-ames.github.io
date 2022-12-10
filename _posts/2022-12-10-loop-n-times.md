---
title: Loop n Times
subtitle: How to repeat a specific section of your flow a fixed number of times
layout: post
---

The technique I am about to describe is not particularly advanced. Anyone could easily come up with it on their own. However, this is a good starting point for me to see how I will approach these topics in my blog, and for you to gain an understanding of what this blog is trying to accomplish. Having said that, let me explain how I encountered this challenge.

The first game I made using Flow Builder was Nim. If you're not familiar with it, Nim is a simple game where players take turns removing objects from a pile until there are none left. The player who empties the pile loses the game.

When I was developing this game, I had the idea of creating a series of Christmas-themed games. I chose to use the emojis 🎄 and 🌲 to represent the pile in the Nim game. The player and the computer will take turns transforming the pine trees into Christmas trees. The player who lights up the last Christmas tree loses the game.

## Create a line of trees

To break the development process into manageable chunks, the first step I took was to create a text variable that represents the trees as a line of concatenated emojis, like this:
```
🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲🌲
```


