---
layout: post
title:      "Makefile 007: Use User Snippets in VS Code for Maximum Efficiency"
date:       2021-06-29 04:48:20 +0000
permalink:  makefile_007_use_user_snippets_in_vs_code_for_maximum_efficiency
---


As the craft person's adage goes, "Take care of your tools and they'll take of you." Today's code development tools allow us to do more with less effort. Nowhere is this more evident than in Microsoft's Visual Studio Code. While their team does its utmost to bring new features to programmers at a rate most of us can't keep up to, there are also improvements we can make on our own.

One of these is User Snippets. You can develop these to conform to your most common use-cases. Why type when you can have the computer type for you?

[Emmet](https://emmet.io/) does a great job in automagically adding code for us, but sometimes we have preferences it just doesn't meet. That's where User Snippets come in.

To create one, just hit the cogwheel at the bottom left of VS Code and select 'User Snippets'. You can make them global, for a particular language, or even for a particular project. Since I've been writing mostly Javascript, many of mine are for that language.

Here's an example:

In a `javascript.json` file I created I made:

```json
  "arrow function": {
    "prefix": "af",
    "body": [
      "(${1:param}) => {",
      "  ${2:body}",
      "};"
    ],
    "description": "Write arrow function"
  },
```

In a js file, if I want an arrow function, I can type `^ + SPACE af` and get

```javascript
(param) => {
  body
};
```

The `$` variables make the magic. I type my param then TAB and type the body.

If I want an arrow function expression, I can deploy my snippet in the same way with `afe` and this snippet

```json
  "arrow function expression": {
  "prefix": "afe",
  "body": [
    "$1 = ($2) => {",
    "  $3", 
    "}$4"
  ],
  "description": ""
},
```

yields

```javascript
 = () => {
  
}
```

I enter the variable name, TAB to the param, TAB again to the body, and yet again to move my cursor to the end.

The snippet I use most is what I call "console.log advanced":

```json
  "console.log advanced": {
    "prefix": "cla",
    "body": [
      "console.log('$1:', $1);"
    ],
    "description": "Log output to console"
  },
```

When I want to console.log, I do `^ + SPACE` and the `cla` prefix and get two cursors for putting in the variable I want to log out. Before the colon I enter the place in the code the log is coming from for clarity.

Another handy one is an "object constructor":

```json
  "object constructor": {
    "prefix": "oc",
    "body": [
      "$1: {",
      "  $2: $3,",
      "},"
    ],
    "description": "Construct an object"
  },
```

Tabbing through takes me from the name of the object to a key and a value.

I also write a lot of Markdown, so in my `markdown.json` I have:

```json
  "Code block": {
    "prefix": "cb",
    "body": [
    "",
    "```",
    "$1",
    "```",
    "",
    "$0"
    ],
   "description": "Make a code block"
	},
```

and

```json
  "URL": {
    "prefix": "url",
    "body": [
      "[$1]($1)$2"
    ],
   "description": "Make a link that shows the URL"
	}
```

which make a formatted code block and url, respectively.

There's no limit to the use cases of User Snippets. Happy coding!
