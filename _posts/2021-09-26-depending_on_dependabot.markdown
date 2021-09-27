---
layout: post
title:      "Makefile 009: Depending on Dependabot"
date:       2021-09-26 23:39:44 -0400
permalink:  depending_on_dependabot
---


***New technologies and approaches are merging the physical, digital, and biological worlds in ways that will fundamentally transform humankind. The extent to which that transformation is positive will depend on how we navigate the risks and opportunities that arise along the way.--Klaus Schwab, German engineer and economist***

## Situation

Looking over my [latest app on GitHub](https://github.com/ronsala/restauranter-frontend) I clicked on the [Dependabot](https://dependabot.com/) tab [Insights > Dependency graph > Dependabot] and was surprised. I have often used Dependabot to keep my dependencies up to date and free of security vulnerabilities. But here I found the message: `Dependabot version updates aren't configured yet`.

## Background

A [little investigation](https://github.blog/changelog/2021-08-03-dependabot-preview-is-shutting-down/) revealed what I'd been using was a preview version that, as of last month, was no longer available. Fortunately, it's been replaced with a still-free [GitHub-native version](https://docs.github.com/en/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/about-dependabot-version-updates).

Beppe Catanese wrote an instructive [blog post](https://medium.com/geekculture/dependabot-is-github-native-only-6b62d048638) about the change. It mentions repos receiving a pull request to automatically switch over to the native version. I couldn't find such a PR in my repo for some reason, but I found setting up the switch myself pretty easy.

## Solution

I just clicked the `Create config file` button under the message mentioned above. This set up a .yml file for specifying options for Dependabot. The only one required for a basic setup is to add the package manager to use in checking for changes in dependencies. Once this file is in master, Dependabot can go to work sending you PRs to update versions of your packages.

I was also able to activate `Dependabot alerts` for vulnerabilities by clicking a button under the GitHub's `Security` tab.

## Recommendation

Dependabot saves me time and gives me peace of mind. I know I'm not alone. If you, like me, missed the change to this valuable service, it's simple to get it running and configure it for your use case.

