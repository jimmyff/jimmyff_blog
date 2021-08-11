---
title: "Painting asteroids"
date: 2021-07-16
draft: false
tags: [gamedev, playdate, lua, space_game]
---

I've been stewing on how I could fill the asteroids to make my [space game](/tags/space_game/) look better. It's a tricky problem as I only know terrain lines and nothing else (so I don't know which side is supposed to be solid and which is supposed to be the empty void of space). This shows what I have and what I want to achieve:

![WEBP](problem.webp "The problem")

I can trust that the space ship will always be in space (even if it's hit an asteroid, it should never actually be in the asteroid!). Using that piece of truth I've came up with an idea, if I projected from the ship to the corners and count the terrain line intersections I should be able to figure out what's solid. If the number of intersections is even, I know the corner should be in also in space, if the intersection count was odd, then the corner is in an asteroid.

![WEBP](possible_solution.webp "Possible solution")

Once I knew if the corners were in an asteroid or not, I should then be able to move along each edge and join up the lines.

## Implementation

![GIF](1-corners.gif "Implementing the intersection counting")

I've implemented the intersection counting, if the line is green then there is an even number of intersections which means the corner is in space, if red then there is an odd number of intersections so this is in the asteroid. 

I've cut the terrain line at the scren edge (and highlighting it with a circle), this is so I can make a nice clean edge on each polygon.

(Oh you might also notice I've implemented asteroid rotation too!)

![GIF](2-triangulate.gif "Implementing the intersection counting")

Here I have implemented the algorithm that combines all the edges in to polygons. At the top there is text that says something like 'P: 2', this means 2 polygons found.

At first I was getting a weird graphical glitch when filling my polygons which I realised was due to the fact my polygons are concave. Filling concave polygons turns out is a technically tricky as the polygon needed triangulating (chopping in to simple triangles). Lucikly Love2d has a triangulate feature that I could use. I coloured the traingles random colours to highlight the trignulation process.

![GIF](3-done.gif "Implementing the intersection counting")

...ta-dah! Here is the finished product. I'm super happy (& surprised) that my crazy idea worked!

I now need to reimplement the ship, but I'm a little hesitant to continue with Lua due to it being so difficult to debug (and I'm really missing static-typing!). I'm thinking about switching to C or possibly Rust to continue my playdate journey.

I apologise for the noisy strangely coloured gif's -I really need to level up by gif skills!
