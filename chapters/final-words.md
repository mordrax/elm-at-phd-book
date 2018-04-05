# Final words

_Two months since starting this "blog post", we are on the cusp of 0.19, our application is approaching 50k LoC and is almost, __almost!__, feature complete for our launch. I reflect on the last 10 months of development and talk about what I think are the strengths and weaknesses of working in Elm professionally._


#### Not a framework

Elm is not a framework. It's not a library. It's a language. Beyond basic necessities like url parsing and rendering to html, we were on our own. The package ecosystem is young and libraries are sparse. This is both a boon and a curse. It takes effort to create all the bits and pieces of a SPA. Experience definitely helps. What we've created works specifically for us and has worked well. We iterate on our libraries as needed, regressions are few and the third party Elm packages that we do use are really solid too.

I've enjoyed the rich package ecosystem on top of the excellent js framework that was MeteorJS before it disintegrated. With React and Angular, finding component libraries was fairly easy. Finding one that was reliable, has up-to-date .ts definitions and did what you wanted, less so. And with Ember, it came with most of what a SPA needed out of the box. I would definitely like to see Elm's package ecosystem mature because I believe the language helps greatly in producing highly reliable packages.

_Aside: When I was making a game using React with react-dnd for drag and drop behaviour, I had frustratingly sunk a week figuring out why I was getting some convoluted error message[^1]. When I was investigating Elm, I didn't find a drag and drop library so I built one, modeled after react-dnd. It has been working fine with no maintenance ever since. That was two weeks into Elm and took me a weekend to write[^2]._


#### Purity, Immutability, ADTs, Compiler ( Elm's quiet heroes )

_No runtime errors!_ is Elm's loud hawker. It boasts: 'come look at this, it runs without errors!'. Whilst this is observably true, I feel like this almost completely misses the point. Runtime errors is but one class of errors that Elm eliminates and it does this as a consequence of a much more significant implication. Elm ensures that _all_ your code paths are handled.

My experience with js and C# is you end up writing a whole suite of unit/integration/component/model tests and the vast majority of things it catches are false positives like from refactoring a function.

In the last 10 months, I've tried to encode as much business logic into ADTs as possible, only hold valid states in our models and the effort has really paid off. Any logic bugs we fix, of course. The rest are typically because the system got into a invalid state or used a poor approximation to an ADT. For these, I change the code to remove the invalid state and represent values correctly. By removing these impossible states, it not only fixes the bug but also eliminates any chance of regression.

I feel that this is the strongest point of the language and the foundation on which everything else rests. In this respect, Elm is in a class of it's own.


#### Responding to business needs, re-designs and regression

We move a lot of code, frequently. Every other week, there would be some sort of refactoring that touches 20-30+ files, makes core changes. The regressions have always been manageable and we've never shied away from doing this because of the fact that we can get away with it each time. So each time, we opt to not carry technical debt because it actually makes more business sense to just do it properly rather that put in a workaround in fear of touching a core system.

On the other hand, you would argue that most core changes ends up effecting a lot of files in the system because type changes propagate to all modules affected. However, this is actually a good thing because the compiler is picking up every possible scenario known to the data types and making sure the program runs 'correctly'. Each `case ... of` or inference error could have otherwise been a much costlier runtime error.

_Aside: I've realised that our triaging of bugs is efficient because it usually takes us about minute to pinpoint the exact one or two places where a bug could occur. So when we triage in standups, it makes that time much more useful to be able to have meaningful discussions and assign work on the spot. Not many items end up as being investigative in nature. As a snapshot, we've got 11 frontend bugs in the whole system! They are all logic errors and the problems are all known._


#### Hiring

This has been a tough one for us. Speaking franky but without saying too much, there is not a large pool of potential candidates for Elm in Sydney. However the _quality_ of candidates seems to be higher so we've been fortunate enough to fill our current needs. (I've only been involved in hiring for one other company so take my words with a grain of salt).


#### So...

I hope this has been an informative read. I'm by no means an expert on Elm or SPAs, but the lack of these kind of long form technical articles is really what drove me to write one. I do wish more people shared their technical challenges and solutions with Elm. There's too many beginner articles with contrived examples compared to more in-depth material.

At the current stage of the project, I'm really happy and comfortable with the team and codebase. We have a handful of bugs, I am refactoring our dropdown component to accept custom default value strings which will affect all our forms. We are a week away from a client demo, I'm not waiting till that is over. Call it what you wish, to me, this is not a risk.

0.19 will come when it does, it doesn't really concern me. Am I excited? Hell yeah! But until then, our team is really happy with how 0.18 is allowing us to rebuild a complex health insurance application at this pace with no compromise on quality.


#### Footnotes


[^1]: Convoluted react-dnd issue, problem could very much be between the chair and keyboard - https://github.com/react-dnd/react-dnd/issues/429
[^2]: Drag and Drop for Castle of the Winds - https://github.com/mordrax/cotwelm/blob/master/src/Utils/DragDrop.elm