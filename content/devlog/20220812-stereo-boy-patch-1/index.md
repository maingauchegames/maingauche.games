---
title: Stereo Boy software update 20220812.f5a7
date: 2022-08-12
draft: false
tags:
- stereoboy
- patch
description: In which we deploy the first patch
---

The first Stereo Boy patch (build 20220812.f5a7) is live on Steam! There’s one significant bugfix, as well as a few quality-of-life improvements. Read on for the changelog.

<!--more-->

## Windows mouse sensitivity fixes

We TOTALLY mangled Windows mouse sensitivity in the launch build! A great way to out yourself as a craven Mac/gamepad user.

Anyway, we turned the sensitivity way down. Hopefully, we were able to dial in something more appropriate for most folks.

## Health bump on retries

If you happen to fail a level, the game will now offer to increase your health.

{{< video-tag "./RetryWithHealth.mp4" >}}

Did you know that you can tweak your health from the settings menu? It goes from 1 HP to 5 HP, plus an unlimited/no-damage option. The default is 3 HP, but go ahead and tune it to your liking. There’s no “right” way to play!

## Quit from pause

You can now quit the game from the pause menu. What a relief!

{{< video-tag "./QuitFromPause.mp4" >}}

## Exit doors are now solid(-ish)

Bullets and pushable blocks no longer pass through the exit door. There's a level or two where this was actually an issue. Hope this doesn’t spoil your amazing speedrun strat!

## Cross-platform mouse sensitivity support

If you are one of those OS-flexible people that play the same Steam games across Windows and Mac, you’ll find that the mouse sensitivity settings are now platform-specific. Your Mac settings won’t get synchronized to Windows, and vice-versa.

## No more infinite laser sight

It was possible in some situations to see the laser sight in both halves of the screen. Kinda ruins the parallel dimension illusion, doesn’t it? Well, we fixed that.

We’re hoping to do a future devlog on how we modeled the parallel world thing, but the presence of this bug is a big hint.

## Settings menu tweaks

- The settings menu has wraparound, so you can easily navigate from top to bottom or bottom to top.
- The pause menu’s settings used to break if you clicked “Back” to exit, and then tried to go back in by pressing spacebar. That’s fixed now.

## Reduced log spam

We fixed an issue that caused the Unity logfile to fill up with a bunch of unhelpful gibberish about navmeshes and non-readable mesh files. You probably didn’t notice this, but it’s the kind of thing that makes our eyes twitch.

For you Unity gearheads out there, this [forum post](https://forum.unity.com/threads/runtimenavmeshbuilder-source-mesh-xxxxxxxxxxxxxxx-does-not-allow-read-access.512563/#post-3353134) describes the fix we ended up pursuing. Feels like a hack! But that’s how it goes sometimes.

## Did we miss anything?

As always, we welcome bug reports and feedback via [Discord](https://maingauche.games/discord), [Twitter](https://twitter.com/maingauchegames), or [email](mailto:info@maingauche.games)!

