# Yet Another Factorio Calculator

> YAFC is a Factorio calculator, planner and analyser. The main goal of YAFC is to cope with heavily modded games.

![Simple usage](/Docs/Media/Main.gif)

YAFC is more than just calculator. It contains multiple analysis algorithms and tries to understand what is going on in your modpack. These analyses go as deep as trying to estimate amount of ores generated by the map generator, and as wide as calculating late-game base trying to figure how much of everything you are going to need. It knows which items are important and which are less important, which recipes are efficient and which are less efficient.

I have started working with YAFC when other tools (such as Helmod) failed to work with deeply recursive Pyanodon recipes. YAFC handles recursive recipes extremely well, it uses [Google OrTools](https://developers.google.com/optimization) as its model solver

YAFC also includes several tools, the most important currently is "Never Enough Items" - it is FNEI on steroids, showing not only recipes to produce or consume an item, but also which recipes you probably want to use, and how much.

> Yafc is currently in early beta, but main functionality is ready to use.

## Project features
- Work with modded games, any mod combination. 
- Multiple analyses:
    - Accessibility analysis: YAFC shows objects that are not accessible. Mods are often hiding objects, and factorio has a bunch of hidden objects (for example campaign entities). Unfortunately it is impossible to find out objects that are spawned by mod or map scripts, this analysis may fail for modpacks like seablock. However, you can mark some objects as accessible manually.
    - Milestone analysis: You can add anything (Item, Fluid, Recipe, Technology, etc) as a milestone. YAFC will display that milestone icon on every object that is locked behind it, directly or indirectly. Science packs are natural milestones, and so they are added by default.
    - Automation analysis: YAFC tries to find objects that can be fully automated. For example, wood in vanilla game cannot be fully automated because it requires you (or bots) to cut trees.
    - Cost analysis: YAFC assigns a "cost" to each object. "Cost" is a sum of "logistic" actions you need to perform to get that object, using the most optimal recipes. YAFC cost is very useful to compare items/recipes/etc at a glance, it is also useful for many heuristics. Also this cost helps to find which recipes are sub-optimal.
    - Flow analysis: YAFC calculates a base that produces enough science packs for all non-infinite researches. So it figures out how much of everything you will probably need
- Dependency explorer tool that allow you to explore dependency graph - ie which objects are needed for what. It can also help debug Milestone, Automation and Automation analyses (find out why YAFC thinks that some object is not accessible for example)
- Never Enough Items Explorer tool that helps to find out how you can produce any item, and also which way YAFC thinks is optimal.
- Main calculator sheet:
    - Setting up links: YAFC will try to balance production/consumption only for linked goods. Unlinked goods are calculated, but no attempt to balance is made. This is very important difference to Helmod that tries to balance anything that have production and consumption, often resulting in infeasibnle model on deeply recuesive recipes.
    - Nested sheets: You can add nested sheet attached to any recipe. When collapsed, you will see summary (all ingredients/products) for all recipes in nested sheet. Nested sheets have also their own set of links. For example, you can create nested sheet for electronic circuits, and putt copper cables production inside that sheet. If you add an internal link for copper cables, it will be separate (so you can calculate separate copper cables for electronic circuits)
    - Auto modules: You can add modules to recipes using single slider. It will automatically add modules you have access to (based on milestones), and it will prioritise putting modules into buildings that benefit the most from them. There is a cool gif of this in action later.
    - Limited support for fluid temperature (without mixing different temperatures) allows to calculate energy generation
    - Fuel (including electricity) is also part of tre calculation - you can even add energy generation exactly enough for your sheet (Inserters are not counted though)
- Supports Factorio versions 0.17+
- Multiple pages
- Undo (ctrl+Z)

## Auto module tool in action
![Auto module tool in action](/Docs/Media/AutoModules.gif)
More gifs can be found [here](/Docs/Gifs.md) (Traffic warning!)

## Possible incompatibilities

YAFC loads mods in an environment that is not 100% compatible with Factorio. I have tested YAFC with some of the most popular mods, but mods are changing and Factorio is changing.
- You (or I) can write mod-specific fixes in lua
- Another way of loading data (directly from the game), is in possible plans
- Anyway, report mods incompatibilities and other bugs in [the issues section](https://github.com/ShadowTheAge/yafc/issues)

> I am playing Seablock / Other "scripted progression" mod and YAFC thinks that items are inaccessible

I don't know any nice solution for this, but you can open *Dependency explorer* and manually mark a bunch of items as accessible (And also starting technologies for Seablock for example)
	
## **[Download YAFC](https://github.com/ShadowTheAge/yafc/releases)**

YAFC is a desktop app. Windows build is the most tested, however OSX and Linux builds also exist. For those OS see [Linux and OSX installation instructions](/Docs/LinuxOsxInstall.md)

## License
- [GNU GPL 3.0](/LICENSE)
- Copyright 2020 © ShadowTheAge
- This readme contains gifs featuring Factorio icons. All Factorio icons are copyright of Wube Software.
- Powered by free software: .NET core, SDL2, Google Or-Tools, Lua and others, [full list](/licenses.txt)