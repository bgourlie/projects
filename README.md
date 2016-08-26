# Elm Projects

This is a big list of Elm projects that are somewhere on a very long todo list.
Many of these ideas are great for contributions and collaborators, so take a
look and see if anything catches your eye!


## Make elm-lang.org responsive

Right now it is not. It would be pretty great if it was! You can check out the code [here](https://github.com/elm-lang/elm-lang.org/).


## Benchmark virtual-dom

The implementation of [elm-lang/virtual-dom](https://github.com/elm-lang/virtual-dom/) should be quite fast. It may be possible to do better though!

**Goal:** Get [elm-lang/virtual-dom](https://github.com/elm-lang/virtual-dom/) setup with [v8-natives](https://www.npmjs.com/package/v8-natives). This would allow us to:

  1. Be sure that code is getting optimized (but not deoptimized!)
  2. Know more about how much garbage is produced.
  
Perhaps certain functions need to be broken into smaller chunks? Perhaps values can be made more monomorphic? A great result would be writeups of what you observe when testing things by hand. If that is useful, it would be best to make these tests a reproducable part of the library. This way any potential changes could be informed by performance implications.


## Improve Process Bot

There is [this robot](https://github.com/process-bot/) that goes around on Elm repos, trying to help issues and PRs go smoothly by letting people know about [the contribution-checklist](https://github.com/process-bot/contribution-checklist). There are two features that I think it would be great to have:

  1. Once a thread gets to 10 posts, process-bot would comment and tell people to close it down and (1) close it down and summarize the state of affairs in a new issue, (2) move the discussion somewhere else until it can be made more clear, or (3) keep talking in the closed thread until you decide to do 1 or 2.
  
  2. When a PR is opened, have process-bot check a list of people who have given contributors agreements. If they have given one, great! If not, give them a message telling them how to proceed.

The relevant code lives in [this repo](https://github.com/process-bot/contribution-checklist).


## Improve Contributor Agreement Process

Right now, you need to find [this agreement](https://github.com/elm-lang/elm-compiler/blob/master/ContributorAgreement.pdf), figure out how to fill it in, and figure out how to get it to me. This process kind of sucks!

There are a couple steps we can take towards improving:

  1. Study how this works in different languages. Python, Clojure, etc. Figure out how they manage it, how much work it is, the particular documents, etc.
  2. Clearly write up the different options and share on the elm-dev mailing list.
  3. After discussion, possibly make some tools to make this easy to track and integrate with process-bot.


## In-browser REPL

This connects back to the Elm Reactor navigation progress a bit, but it can be done totally independently as well.

Some modules are best examined with the time-traveling debugger, others are best examined by poking around with certain functions. It would be extremely cool if we had an in-browser REPL so that we could do either. This would let us show `Element` and `Html` values really easily!

This is super free-form. Maybe inspiration can come from iPython.


## Improve Elm Reactor Navigation Page

Thanks to @JustusAdam and this repo, [Elm Reactor](https://github.com/elm-lang/elm-reactor)'s navigation page has undergone a really nice visual overhaul! There are still some cool things we can do though:

  1. Figure out if new versions of packages exist and give notifications. Maybe have information about upgrade costs based on API diffs and number of uses of changed or removed values.
  2. Make possible to read documentation for packages *without* an internet connection.


## Visualize Compilation

It would be cool if when you compile your code, you get a nice dashboard that shows you what is going on and helps you fix any problems that may exist. We could show all the dependencies of the project as a very cool progress bar:

![dependency graph progress](https://raw.githubusercontent.com/elm-lang/projects/master/compiler-progress-visualization/mock.gif)

Notice that we can keep compiling files even after one failed if they do not depend on each other. We could make it so a user would click on a red node to get a in-browser panel about that module and what the particular errors were. This way, doing a refactor does not require going back to the compiler tons of times, you just run it and fix everything that is red!

Maybe we could also add information about build statistics. Which modules are slow? Are there bottlenecks in the dependency graph that lead to less parallelization? I think this could be cool on really large projects when you want to do tricks to bring down compile times.

If you work on this, **start with the UI**. Do not worry about integration at first. I would expect the steps to be:

  - Make a library for visualizing dependency graphs. Probably with SVG.
  - Use dummy dependency graphs and script dummy events to see things flow through.

If this works, you will definitely have a cool library. From there, we can figure out how to get `elm-make` producing the necessary information.
