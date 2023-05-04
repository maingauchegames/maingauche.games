---
title: Counting allocations in Unity
date: 2023-05-04
draft: false
tags:
- unity
description: Treat your GC with kindness.
---

Have you ever wondered how many heap allocations your C# code is making? Here’s a little class called [AllocCounter](https://gist.github.com/jeffomatic/cfa560bad7a1163730d1b5f75f549f93) that will help you do that. It’s pretty straightforward:

```csharp
var ac = new AllocCounter();

// code that may or may not do allocations

var allocCount = ac.Stop();
```

If you like lambdas, you can use this style as well:

```csharp
var allocCount = AllocCounter.Instrument(() => {
  // code that may or may not allocate
});
```

<!--more-->

Why would you want this? Spend any amount of time in a Unity forum and you’ll find someone loudly admonishing you to eliminate frame-over-frame allocations from your code. This is probably good advice, but also a particularly masochistic proposition given that we’re using C#, a language that often seems purpose-built for making allocations.[^1]

How one goes about eliminating allocations is largely a matter of finding them in the first place, and on this topic, the advice comes with far less bravado and far more hand-waving. As far as I can tell, solutions fall into one of two camps:

1. You can memorize a bunch of [granular arcana](https://www.sebaslab.com/zero-allocation-code-in-unity/) about which language constructs do allocation (`class`, lambdas, `foreach` [sometimes](https://stackoverflow.com/questions/18552669/memory-allocation-when-using-foreach-loops-in-c-sharp)). Good luck learning about them all, let alone remembering them!
2. You can bust out with the Unity profiler and try to read the tea leaves from ten thousand feet above your code. The profiler is geared toward finding averages over time, rather than providing exact samples over a particular code path. Also, I tend to only reach for the profiler under duress; it’s slow and wonky and generally a huge bummer to interact with.

Anyway, I often find myself wanting something that’s more empirical than the first thing, and more precise than the second. Say you wrote a new component, and you wonder if you added more allocations. Or, you caught an allocation hotspot in the profiler, but you need to drill down with more detail. When you want to measure how _long_ something takes, the easiest method is to add a bit of code that records the start time, and then subtract that from the end time. Surely we can do something similar with allocations?

In this era of forum bitrot, decaying search engines, and even worse AI suggestions, it was surprisingly hard to find advice on which API to use for this. Then I had a lateral thought: if having zero allocations was so important to the Unity developer community, surely there is a way to write unit tests for that. And it turns out a solution for that problem comes from Unity’s own house. Behold, a very long identifier: [UnityEngine.TestTools.Constraints.AllocatingGCMemoryConstraint](https://docs.unity3d.com/Packages/com.unity.test-framework@1.1/api/UnityEngine.TestTools.Constraints.AllocatingGCMemoryConstraint.html).

Peeking under the lid, you can see that the allocation test constraint boils down to a [scant 4-5 lines of code](https://github.com/gregoirerosier/GAME-DEV/blob/ef217db2a5de51b54e5ed5399b10a745b84d6387/AllocatingGCMemoryConstraint.cs#L27-L55) that are 100% portable to a runtime context. Indeed, `AllocCounter` is little more than a copy/paste. It turns out the Just Use The Profiler camp was correct, sorta: this trick relies on some instruments exposed by the profiler _library_.

`AllocCounter` is a handy tool that I look forward to using when the bell tolls and I’m finally asked to account for my reckless use of Linq and `IEnumerable` in our game code. But before that day comes, I also enjoy using it to discover some fun trivia about C#. For example, did you know that creating a [value tuple](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-tuples) like `(1, true, "foo")` actually *does* allocate memory? You get exactly _one_ allocation the first time you create a tuple with a particular type signature. My theory is that it’s allocating some kind of type descriptor or metaclass-like thing so the runtime knows what to do with the value in certain contexts.

Discuss on [Discord](http://maingauche.games/discord) and [Reddit](https://www.reddit.com/r/Unity3D/comments/137v1s5/counting_allocations_in_unity/). We'd love to hear from you!

[^1]: Consider that one of the C# designers has an article about the language called ["The stack is an implementation detail"](https://learn.microsoft.com/en-us/archive/blogs/ericlippert/the-stack-is-an-implementation-detail-part-one).