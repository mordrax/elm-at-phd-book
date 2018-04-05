# Final words

_Two months since starting this "blog post", we are on the cusp of 0.19, our application is approaching 50k LoC and is almost, __almost!__, feature complete for our launch. I reflect on the last 10 months of development and talk about what I think are the strengths and weaknesses of working in Elm professionally._

So, what was originally just a blog post, has definitely turned out a fair bit longer than I had expected. Yet I still feel like I hadn't covered everything, such as page loading and routing, boilerplate state wiring ( especially for UI components ), the tendency for business logic to be 'lost' in functions in different modules, collaborating on a Elm codebase when major refactors are happening, testing, regressions and the list will probably go on for a while.
Hopefully what I have written about, will give an idea of what it's like writing an application in Elm.


#### Not a framework

Elm is not a framework. It's not a library. It's a language. Beyond basic necessities like url parsing and rendering to html, we were on our own. The ecosystem is young and libraries are sparse. This is both a boon and a curse. It takes effort to create all the bits and pieces of a SPA. Experience definitely helps. What we've created works specifically for us and has worked well. We iterate on our libraries as needed, regressions are few and the third party Elm packages that we do use are really solid too.

I've enjoyed the rich package ecosystem that was MeteorJS before it disintegrated. With React and Angular, finding component libraries was fairly easy. Finding one that is compatible and did what you wanted, less so. And with Ember, it came with most of what a SPA needed out of the box. I would definitely like to see Elm's package ecosystem mature because I believe the language helps greatly in producing highly reliable packages.

_Aside: When I was making a game using React with react-dnd for drag and drop behaviour, I had frustratingly sunk a week figuring out why I was getting some convoluted error message[^1]. When I was investigating Elm, I didn't find a drag and drop library so I built one, modeled after react-dnd. It has been working fine with no maintenance ever since. That was two weeks into Elm and took me a weekend to write[^2]. I've never felt like I could write a production ready OSS library until that point._


#### Purity, Immutability, ADTs, Compiler ( Elm's quiet heroes )

_No runtime errors!_ is Elm's loud hawker. It boasts: 'come look at this, it runs without errors!'. Whilst this is observably true, I feel like this is _completely_ missing the point. No runtime errors are but one ( arguably ) minor side effect of what Elm truly offers, the ability to _avoid_ most classes of errors. Typos, null references, wrong type of arguments, array overflows, uncaught exceptions, callbacks overwriting data are just some of them. What about forgetting to handle certain business cases? How about a logic error in the runtime state such as a user logged in but without a valid JWT?

My experience with js and C# is you end up writing a whole suite of unit/integration/component/model tests and the vast majority of things it catches are false positives like from refactoring a function. In the last 10 months, I've spent most of my time avoiding these types of errors, not writing these kinds of tests _and_ I have absolute certainty that the product won't break in these ways because it is impossible.

In my time with the project I've only fixed logic bugs. When we encounter a bug created by invalid state or poor use of types, I refactor instead and make it impossible to ever get into those states again thus eliminating any possible chance of regressions.

I feel that this is the strongest point of the language and the foundation on which everything else rests. For this point, Elm is in a class of it's own.


#### Re-designs, coding and regression

We move a lot of code, frequently. Every other week, there would be some sort of refactoring that touches 20-30+ files, makes core changes. The regressions have always been manageable and we've never shied away from doing this because of the fact that we can get away with it each time. So each time, we opt to not carry technical debt because it actually makes more business sense to just do it properly rather that put in a workaround in fear of touching a core system.

On the other edge of this sword, you would argue that most core changes ends up effecting a lot of files in the system because the same reasons that makes the application stable also means the compiler is making sure the program still runs 'correctly' meaning, all the ADTs, function return values, msgs still match. This is a good thing, because each inference or unhandled case of error that the compiler picks up would have been a runtime error costing so much more human time and effort to fix.

_Aside: I've realised that our triaging of bugs is efficient because it usually takes us about minute to pinpoint the exact one or two places where a bug could occur. So when we triage in standups, it makes that time much more useful to be able to have meaningful discussions and assign work on the spot. Not many items end up as being investigative in nature. As a snapshot, we've got 11 frontend bugs in the whole system! They are all logic errors and the problems are all known._


#### Hiring

This has been a tough one for us. Speaking franky but without saying too much, there is not a large pool of potential candidates for Elm in Sydney. However the _quality_ of candidates seems to be higher so we've been fortunate enough to fill our current needs. (I've only been involved in hiring for one other company so take my words with a grain of salt).


#### Final final sentence

If I had to create results quickly, have it react to complex and changing business requirements but not break every time, work with very limited resources (human) and produce a stable, maintainable product, you know what I'd pick.


#### Footnotes


[^1]: Convoluted react-dnd issue, problem could very much be between the chair and keyboard - https://github.com/react-dnd/react-dnd/issues/429
[^2]: Drag and Drop for Castle of the Winds - https://github.com/mordrax/cotwelm/blob/master/src/Utils/DragDrop.elm