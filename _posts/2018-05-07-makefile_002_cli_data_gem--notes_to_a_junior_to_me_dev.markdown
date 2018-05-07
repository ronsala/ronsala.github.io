---
layout: post
title:      "Makefile 002: CLI Data Gem--Notes to a junior (to me) dev"
date:       2018-05-07 07:13:37 -0400
permalink:  makefile_002_cli_data_gem--notes_to_a_junior_to_me_dev
---

*I have not failed. I've just found 10,000 ways that won't work.*—Thomas Edison

I recently finished the (pre-assessment) code for my CLI Data Gem, the first of the portfolio projects in the web dev curriculum at Flatiron School. Not only is it my first Ruby gem, it’s the first program of any sort I’ve made that wasn’t part of a more prescriptive tutorial or lab. Here, for the first time, within some very broad parameters, I was free to use my creativity to come up with a vision and work it out in code. 

I felt quite humbled that I wasn’t as solid on many of the concepts from previous lessons as I’d thought I was. Instead of concentrating on just one (or at most a few) key ideas, as in the preceding labs, I had to make it all work, based on what had come before and learning as I programmed. It’s as if, as a culinary student, after lessons on preparing individual ingredients, I was now presented with the whole kitchen and told, “Make a meal.” For me, it was a transformative experience.

If I’d had it to do over, what’s some advice would I give the slightly more junior dev I was then?

**Take notes**

I’ve heard this recommended and want to try it on future projects. If I’d made some short notes as I programmed--on sticking points, solutions, resources--I’d have a clearer picture about the whole process and how I could approach similar situations later. Also, I'd have material I could draw on for blog posts and other opportunities to help fellow programmers. 

**Pay attention to separation of concerns early**

My gem is a quiz game that scrapes a dictionary site to present multiple choice questions to the user. Early on, I had three classes, CLI, Question, and Scraper. 

Having trouble getting these classes to work together (see Scope, below), I tried merging together the code from Scraper into Question. One of the tech coaches persuaded me to separate them out again, with Scraper only concerned with scraping and Question only concerned with forming questions. Later, another coach suggested moving some additional code from one class to another for an even clearer separation of concerns. 

I found these migrations a lot more complex than just copy and paste because I needed to get all the logic to work in the new configuration. I'm glad I was given this advice, though. Besides it being something assessors look at, I could see how a larger project could easily become unwieldy without clearly designating what discrete pieces of code do. If I'd been more intentional about this from the beginning, I'm confident the coding would have been quicker and easier. 

**Know your scope**

Many of my sticking points came from being unclear about what levels of scope were operating at given places in the code. For instance, I spun my wheels for a while under the mistaken idea that I could directly access a variable from one class in another. (I needed to access them via methods). I recommend a handy illustrated guide: ([http://www.sitepoint.com/understanding-scope-in-ruby/] “Understanding Scope in Ruby”) by Darko Gjorgjievski. Many of my sticking points came from being unclear about what levels of scope were operating at given places in the code. For instance, I spun my wheels for a while under the mistaken idea that I could directly access a variable from one class in another. (I needed to access them via methods). I recommend a handy illustrated guide: ([http://www.sitepoint.com/understanding-scope-in-ruby/ “Understanding Scope in Ruby”) by Darko Gjorgjievski. 

**Use a linter**

I was using the (https://code.visualstudio.com/ "Visual Studio Code IDE") for the first time for this project. Part way through coding, I upgraded to the new version and started to see green lines under parts of my code. It turns out this was a linter. Specifically, it was using (http://rubocop.readthedocs.io/en/latest/ "Rubocop"), which gives suggestions based on the community (https://github.com/bbatsov/ruby-style-guide "Ruby Style Guide"). It flagged when classes, methods, and lines were too long or complex, indentation was misaligned, there was useless variable assignment, and much more. It’s like having a pair programmer inside the computer, and it helped me use best practices, some of which I hadn't even been aware of. It also integrates with Atom and many other tools. 

**Hold your head up!**

For me, this project was as challenging psychologically as it was technically. It took me much longer than I'd anticipated. Just when I thought I had everything under control, there'd be another error, edge case, or unfamiliar concept. More than once I wondered if I had what it takes to be a programmer. Flatiron staff and students were of great value to me, as was encouragement from family and friends, and spiritual practice. Even waking away for a while to clear my head helped. If you find yourself in a similar place, remember, it gets better. And, you’ll find yourself a stronger dev, and person, than you were before. 

