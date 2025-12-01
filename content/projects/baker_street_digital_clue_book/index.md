---
title : 221B Baker Street Digital Clue Book
type : project
date: 2025-11-25
categories: ["showcase"]
tags: ["web app", "Javascript", "CSS", "HTML", "quality-of-life"]
draft : false
description : A quality of life web application to quickly search clues from the 221B Baker Street board game by Gibsons Games.
---

## The problem

221B Baker Street is a fun board game. 

<figure>
    <img style="display: block; margin: auto; width: 50%" src="https://cf.geekdo-images.com/QHJF0yoyIW8WGprJRwbMsQ__imagepage/img/cGSkISpWiM775s8shyPHeR9cLmk=/fit-in/900x600/filters:no_upscale():strip_icc()/pic2235991.jpg"/> 
    <figcaption style="text-align: center">
        The 221B Baker Street board game box. 
        <a href="https://boardgamegeek.com/image/2235991/221b-baker-street-the-master-detective-game" target="_blank">
        {{< icon "external_link" >}}
        </a>
    </figcaption>
</figure>

The goal is to identify the criminal, motive and weapon used in a crime. The first player to do so is the winner.
Players take turns rolling a die and move around various places to look for clues. These clues are stored in a paper clue book.

<figure>
    <img style="display: block; margin: auto; width: 30%" src="
    https://cf.geekdo-images.com/m-2IC740v1Y2AncUsRE-pg__imagepage/img/zmBPTKPIQaUjK1CXXtiY-byj-ZA=/fit-in/900x600/filters:no_upscale():strip_icc()/pic2958732.jpg"/> 
    <figcaption style="text-align: center">
        The 221B Baker Street board game box. 
        <a href="https://boardgamegeek.com/image/2958732/221b-baker-street-the-master-detective-game" target="_blank">
        {{< icon "external_link" >}}
        </a>
    </figcaption>
</figure>

Unfortunately, searching through this clue book is a tedious process, as you can imagine. This is especially true with a high player count.

So how would you allow players to:

- simultaneously have access to the clues
- reduce the time it takes to search for the right clue
- ensure each player does not read a clue longer than the allocated time?

My solution is to design a web application where players can:
- each have a copy of the clues
- keep track of their reading time
- search for a clue by number instantly.

All that is required on the part of the players is a wifi capable device with a browser.

## A quality-of-life improvement


<video style="display: block; margin: auto" width="40%" controls>
<source src="clue_book_demo.webm" type="video/webm">
Your browser does not support the video tag.
</video>

That was the app. The music is a bit over the top, but I think it captures the sense of urgency pretty well. 

You would've noticed a scanned page being displayed after the submit button was pressed. This is because the clues are a collection of scans from the physical clue book. There are 1050 clues in the book, stored within 86 pages.

Yes, I did have to scan the whole book, however, I scanned two pages at a time and digitally split them into two. This did not take too long, suprisingly. More importantly, this only needed to be done once.

Each file was renamed to include the range of clues it held. For example, if a page held clues 1 to 30, it would be renamed to ```clue_1_30.jpg```.

To identify the appropriate clue page given an input clue number, the web app extracts the clue range from the file name using simple regex, and checks if the input clue number is within the range.

There is the possibility of a clue spanning two pages, that is why the web app checks all the file names and does not stop at the first match. The web app could be improved by stopping after the second match, however, the performance is sufficient and optimisation isn't really required for my use case.

In other words, once it was working, I didn't modify the code for optimisation. My goal was to finish this project within a day. If it met all the requirements and was perfomant enough, it would be enough for me.

## Logic diagram
The logic flow of web app is simple.

<div style="display: block; margin: auto; width: 80%">
{{< plantuml id="webapp" >}}
[*] --> Homepage
Homepage --> validInput: submit button pressed
validInput --> Cluepage : input is valid
validInput --> Homepage: input is invalid
Cluepage --> Homepage : count down ended OR cancel button pressed

Homepage: Display submit button
Homepage: Display input clue number
Homepage: Play countdown ended music (if coming from clue page)

state validInput <<choice>>

Cluepage: Display scan containing clue number
Cluepage: Display cancel button
Cluepage: Timer counter down
Cluepage: Play panic music

{{< /plantuml >}}
</div>

## Project Resources

<a href="https://github.com/jensen-benard/baker-street-clue-book-web-app" target="_blank"> Web app github repository {{< icon "external_link" >}} </a>


## External Links
<a href="https://boardgamegeek.com/boardgame/1275/221b-baker-street-the-master-detective-game" target="_blank"> About the 221B Baker Street Board game {{< icon "external_link" >}}</a>