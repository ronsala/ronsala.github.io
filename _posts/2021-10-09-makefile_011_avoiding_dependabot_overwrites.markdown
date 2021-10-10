---
layout: post
title:      "Makefile 011: Avoiding Dependabot Overwrites"
date:       2021-10-10 00:52:01 +0000
permalink:  makefile_011_avoiding_dependabot_overwrites
---


***Доверяй, но проверяй (Trust, but verify)--Russian proverb***

## Situation

After stepping away from my [Restauranter](https://github.com/ronsala/restauranter-frontend) project for a few days, found several pull requests from GitHub's Dependabot.

## Background

Had a bad experience with Dependabot on another project when I pulled in one of its PRs after my own and found my own work eliminated since Dependabot was using a previous version of my repo when it was doing its work. Furthermore, I've adopted the ethos of not putting anything into master that I can't verify is working, i.e. it passes the test coverage I've created.

## Assessment

Wanted to be able to verify the advice on package updates Dependabot was giving me to make sure I could still pass my Cypress tests.

Pulled my repo to my local machine. In the command line saw it had pulled down all the branches Dependabot had made since my last contribution. Following [Checking out pull requests locally - GitHub Docs](https://docs.github.com/en/github/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/checking-out-pull-requests-locally), tried to check out one of the new branches:

```zsh
gh pr checkout 76
```

Was prompted to install GitHub CLI:

```zsh
brew install gh
```

After following the instructions to authenticate, repeated previous command and was able to successfully test the package upgrade Dependabot had recommended.

Realized Dependabot had used my current `master` branch as the baseline for all its package upgrade PRs and didn't want to overwrite any changes I was making. Went to my `package.json` and removed some packages marked for upgrade I didn't think I needed and updated the rest. Tested again. Tests passed. Checked out a new `package-update` branch, committed, pushed, and pulled it to `master`.

## Recommendation

Setting up continuous integration on GitHub should be an easier way to ensure code functionality while staying up-to-date. (I had looked at the starter workflows on GitHub but didn't see one for React or JavaScript). This is a workflow that, though somewhat tedious, gets the job done. I offer it for your consideration.

