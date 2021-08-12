---
title: "Building a web app, the progressive way"
date: 2018-06-25
draft: false
tags: [dart, web, eurovision, app]
---

__And finding an unconventional solution to a challenging objective__

(_I've also posted this article [over on Medium](https://medium.com/@jimmyff/building-a-web-app-the-progressive-way-e81177e95738)._)

As a passionate developer I’m aways juggling side projects alongside my pay-the-bills work. Earlier this year I secured some great tickets to the Eurovision Song Contest and in the excitement I decided to build a modern web app to explore and discover the history of the annual show. I set myself some objectives:

- It should utilise the very latest and greatest web technology.
- It should contain Eurovision Song Contests historic results and the information should be available in the most used languages in Europe.
- The data must be easy to maintain (this was the tricky bit!).

_Tldr: ~~Here’s the app~~ (as of 2020 I've retired this version in favour of my newer flutter app) I built and below are the details of how I put it together & the challenge I encountered, video demo at the bottom._

![WEBP](eurovision_app.webp "The finished app")

## A progressive app and a progressive attitude

‘Progressive Web Apps’ (or ‘PWAs’) are essentially shining exemplars of modern web technologies. They feel more like native apps than they do their creaky website ancestors. PWAs have the ability to work offline, be installed on your devices, and even receive push notifications. I’m a huge advocate of PWAs and I’ve done talks on the subject for my local tech community.

Over the last year a large part of my everyday work has been building a large PWA to replace a complex established website. For my new Eurovision pet-project I wanted something much leaner and simpler. As well as building the app as PWA, I would challenge myself to approach every decision from the UI to the back-end with a modern progressive attitude.
A progressive language & framework

My language of choice is Dart. It’s strongly typed, fully object orientated and a language that makes me really productive. For web it compiles down to JavaScript. You can even use it to build native mobile apps with Flutter or run Dart on your server or development machine using the Dart VM -it’s the genuine holy grail!

For the framework I chose Angular Dart, it’s a great framework that allows you to build robust and sophisticated web apps in a structured and opinionated way. I utilised ‘angular_components’ which are the same battle-hardened material design components that Google use on their own products. I also used the ‘intl’ library which allowed me to extract the text into dictionary files which could then be translated in to various languages.

## Backend as a service

In keeping with the progressive philosophy I chose Firebase for the backend. Firebase is a fully managed platform for building applications, these kind of platforms are often referred to as ‘backend as a service’ (‘baas’). With a solution like this, the jobs that traditional servers would do are broken down in to numerous services and you simply pay for what you use. It’s a really hassle-free, modern & progressive approach to application infrastructure and I love it!

## The challenge of maintaining the data

The biggest challenge I faced building this app was how to maintain the data. I really wanted a simple and elegant solution to updating the app but my choice of database-technology made this tricky. As I was using the Firebase backend I choose to use its new fancy Firestore database, however this is a ‘NoSQL’ datastore that doesn’t allow realtime complex querying or aggregating of data across relationships. I would be storing data that has lots of relationships and needed lots of aggregated statistics. Ideally I‘d use a relational database for this kind of dataset but as my objective was to be modern, simple and progressive, I really wanted to avoid the traditional database+server combo.

Using Firestore meant I would need to compute all the relationships in my data ahead of time and cache these relationship & aggregated values in my data objects. Doing this also makes updating the data challenging as changing one object would likely have knock on effects to other objects that held a cache of the modified data.

## A frugal solution

The solution I came up with to maintain the data was to export it all to a Google Spreadsheet (yes …you read that correctly) and this would become my ‘source of truth’. Using the Spreadsheet I could then rebuild my database whenever required. I essentially use Firestore as a glorified cache. It feels like an unconventional yet rather elegant solution. Here’s is a breakdown of the build process:

1. Download the CSV files from the Google spreadsheet.
2. Using the CSV files rebuild all the objects.
3. From ‘Firebase Cloud Storage’ download the current snapshot of all the objects that are currently stored in the database.
4. Diff the newly built objects with the downloaded database snapshot.
5. Prompt the user with a summary of changes asking them if they wish to apply these changes.
6. Apply the diff to the Firestore database.
7. Upload the newly built objects to ‘Firebase Cloud Storage’ as the latest database snapshot. This will be used next time the build process is run.

I love this solution for the following reasons:

- I didn’t have to write loads of data-management code: logic, forms, validation etc. I just setup some validation rules and conditional formatting on the spreadsheet. This left my codebase nice, clean and simple.
- Rebuilding from scratch every time inadvertently solves one of my main gripes with NoSQL data stores: when you refactor your data structures you can end up with inconsistencies across a collection due to the lack of collection-wide schemas. This mitigates the problem by simply patching any changes you make across the entire dataset.
- The thing that blows my mind is that this runs in the client browser (as there is no conventional server in this equation). It feels like only a short-while ago that browsers would struggle to do anything complex client-side and now they’re capable compiling thousands of objects from a remote collection of CSVs, diffing, patching then reuploading without even breaking a sweat. The entire process takes seconds to run and it builds and diffs over 3,000 objects. It also feels a really simple, efficient & frugal solution to harness the processing power of the administrators device & browser.

## The finished app

<div class="youtube">{{< youtube -MPWaxSBLPo >}}</div>

~~You can try the finished app here~~ (as of 2020 I've retired this version in favour of my newer flutter app). It’s been so much fun to approach a project with a progressive attitude and a fresh set of eyes. I enjoyed it so much I’ll continue to develop the app (and I have some great ideas for it). I also plan to do more projects like this over the next 12 months so watch this space!