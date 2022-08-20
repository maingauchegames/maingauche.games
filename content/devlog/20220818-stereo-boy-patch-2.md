---
title: Stereo Boy software update 20220818.d2b5
date: 2022-08-18
draft: false
tags:
- stereoboy
- patch
description: In which we deploy the second patch
---

The second Stereo Boy patch (build 20220818.d2b5) is [live on Steam](https://store.steampowered.com/app/2073530/Stereo_Boy/)! This one is mostly fixes for bugs you probably *felt* more than noticed. Read on for the changelog.

<!--more-->

- The Stereo Boy logo had a bug! The letter “O” was getting cut off a little on the top. Can’t unsee! Thankfully, it’s now fixed.
- The arrow icons that show you which directions you can push stuff are more responsive. There was a bug preventing them from refreshing properly.
- Mouse users rejoice! Some menu buttons were hard to click, like the social media links and the adjustment arrows in the settings menu. Hopefully they’re a bit easier to work with now.
- There was a funny issue where stacks of teleporting blocks would not illuminate or darken in sync. That’s fixed now! The logic has always been based on which blocks are allowed to teleport, but it gets pretty complicated when you add stacking to the mix. Could be a good subject for a future blog post, hmm…🤔
- Both PC and Mac builds are now code-signed. On top of being good developer hygiene, code-signing can prevent some scary warnings from anti-virus software. In the long run, it also makes it possible to let people download the game from a web page. We’re only on Steam now, but who knows? Maybe [itch.io](http://itch.io) could be a nice DRM-free alternative.
- Blit’s laser sight is no longer obstructed by visual decorations. This might end up looking weird in some cases, but we figured that if these decorations don’t block your shots, they probably shouldn’t block the laser sight either.
- For the hackers out there: the game used to steamroll your save data if it detected an invalid format. We have since taught it some manners. Now, it’ll politely back up your old file, and start with a new, blank file.
