---
layout: post
title:      "Makefile 008: Help! I Have Two Package Managers"
date:       2021-09-20 02:55:03 +0000
permalink:  makefile_008_help_i_have_two_package_managers
---


***"No one can serve two masters."--Jesus***

While building a React app for my final project at Flatiron School, I became aware I'd committed something of a coding gaffe. Following various examples and advice on the net, I'd included both npm and yarn as package managers.

Whether to use one or the other (something else) is as lively a discussion as [Spaces vs Tabs](https://youtube.com/clip/UgxZR7ij4IUfP8Huux54AaABCQ). (From study group discussion, I know I'm not the only one to have done this.) But it seems the consensus of coders is not to. Even yarn warned me not to. There is even a risk of the dreaded [Dependency hell](https://en.wikipedia.org/wiki/Dependency_hell) where packages don't get along and create chaos.

What to do?

This is what I did to remove yarn, as it seems to me it's not cited as much as npm, and as a recent code school grad I rely heavily on others' examples:

Simplified summary of commands, using zsh:

```zsh
rm yarn.lock
npm i
```

I caused the app to rely only on npm. Afterward, I did have some difficulty getting a couple of packages to work, but since I was meaning to remove them eventually anyway, I did so and got the app working without too much difficulty. All in all, I think it was well worth the anxiety of the moment for a more stable experience.

