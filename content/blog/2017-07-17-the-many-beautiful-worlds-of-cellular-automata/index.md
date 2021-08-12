---
title: "The many beautiful worlds of Cellular Automata"
date: 2017-07-17
draft: false
tags: [cellular_automata, dart]
---

I've been interested in Cellular Automata (such as 'Conway's Game of Life') for years. I've implemented them countless times in various programming languages. A couple of weeks back I created a [Dart library](https://pub.dev/packages/cellular_automata) for exploring playing with Cellular Automata, it's open source and [available on Github](https://github.com/jimmyff/cellular_automata). You can browse the [demos on github](https://jimmyff.github.io/cellular_automata/) or see the library running on my personal website -the gifs on this article were also generated using the library.

![GIF](1.gif#pixelate "Cellular Automata rule set: 'Star Wars' with a random seed")

## What are Cellular Automata?

Cellular Automata were all the rage in Science and Math clubs back in the 70s & 80s however the first papers on the subject actually date way back to the 40s. In those days mathematicians & scientists created the rules using pen and paper rather than a computer (John Conway actually created his 'Game of Life' rules on a Go board!). Stephen Wolfram wrote numerous papers on the subject in the 80s & 90s.

A Cellular Automaton is a grid of 'cells', each of which has a single 'state'. For each cycle (known as a new 'generation') a set of rules are applied to each cell in the grid which could potentially change it's state. The rules usually consider each of the cells 'neighbourhood' (the surrounding cells). Cellular Automata rules are usually incredibly simple. Below are the rules to 'Conway's Game of Life' ([here is my library's code implementation](https://github.com/jimmyff/cellular_automata/blob/master/lib/src/rules/game_of_life.dart)):

- Any living cell with fewer than two live neighbours dies, as if caused by underpopulation.
- Any living cell with two or three live neighbours lives on to the next generation.
- Any living cell with more than three live neighbours dies, as if by overpopulation.
- Any dead cell with exactly three live neighbours becomes a living cell, as if by reproduction.

![GIF](2.gif#pixelate "'Conway's Game of Life' with a patterned seed")

'Conway's Game of Life' (among many other rules) can be described as [Turing-complete](https://en.wikipedia.org/wiki/Turing_completeness), meaning they can perform computations (if the necessary cell states are in particular formations — [like this](http://rendell-attic.org/gol/tm.htm)). [Wire World](https://en.wikipedia.org/wiki/Wireworld) is another incredibly simple rule that allows the simulation of electronic logic elements —the 80s equivalent of Minecraft's redstone circuits!

What fascinates me is that from such a simple set of rules, complex systems can arise. Often stable groups of cells occur and large complex formations that can even move as a single unit. Reoccurring patterns arise that can span numerous generations (there's a simple 3 generational pattern in the header graphic). I find this aspect of Cellular Automata so exciting -you never know what you are going to see. It's as if we're simulating a very basic universe. What would happen if rather than a very simple 2D grid of cells, we simulated protons, neutrons & electrons? Would we also see complex structures appear; or even simulated life? (aside: [Simulation hypothesis](https://en.wikipedia.org/wiki/Simulation_hypothesis))

## The Dart library

The library separates the Cellular Automata rules (the fun bit) from the boilerplate processing & rendering. This makes it quick & easy to add new rules or experiment. I've added a few rules so far and also added support for 'MCell' rules so it can run any of the hundreds of rules published in the [MCell rules Lexicon](http://www.mirekw.com/ca/rullex_rtab.html). I plan to add the ability to have numerous rule sets running in the same scene although this feature will have to wait for a rainy day. The rendering code is also decoupled which means you can easily add/swap renderers as you need, I've already added a few (WebGL, Canvas, Html) and I plan to add another that can drive an LED Matrix.

![GIF](3.gif#pixelate "'Brain's Brain' with a patterned seed")

The dart package 'cellular_automata' is published on [pub.dartlang.org](https://pub.dev/packages/cellular_automata). Have fun with it and don't forget to send me a pull request! ;-)