# Final words

_Two months since starting this "blog post", we are on the cusp of 0.19, our application is approaching 50k LoC and is almost, __almost!__, feature complete for our launch. I reflect on the last 10 months of development and talk about what I think are the strengths and weaknesses of working in Elm professionally._


#### Not a framework

Elm is not a framework or a library. It's a language. Beyond basic necessities like url parsing and rendering to html, we were on our own. It takes effort to create all the bits and pieces of a SPA, things such as routing, page loading, error notification and handling, mapping view models, forms, validation, optimistic data loading etc. Experience knowing what is needed definitely helps. What we've created works specifically for us and has worked well. We iterate on our libraries as needed, regressions are few and the third party Elm packages that we do use are really solid too.

I've enjoyed the rich package ecosystem on top of the excellent js framework that was Meteor before it disintegrated. React and Angular has a bountiful supply of components but picking a stable one that does what you want is more tricky. And Ember comes with most of what a SPA needed out of the box. So I would definitely like to see Elm's package ecosystem mature because the language greatly helps in producing highly reliable packages.

_Aside: When I was making a game using React with react-dnd for drag and drop behaviour, I frustratingly spent a week trying to figure out some convoluted error message[^1]. Never really got to the bottom of the bug, just ended up avoiding it. When I was investigating Elm, I didn't find a drag and drop library so I built one, modeled after react-dnd. It has been working fine with no maintenance ever since. That was two weeks into Elm and took me a weekend to write[^2]._


#### Purity, Immutability, ADTs, Compiler ( Elm's quiet heroes )

_No runtime errors!_ is Elm's loud hawker. It boasts: 'come look at this, it runs without errors!'. Whilst this is observably true, I feel like this almost completely misses the point. Runtime errors is but one class of errors that Elm eliminates and it does this as a consequence of a much more significant implication. Elm ensures that _all_ your code paths are handled. This is why throughout the article, our solution has repeatedly been to prefer ADTs to model data, remove impossible state. The more domain logic that is encoded in your types, _the more that Elm will handle your domain logic_!

This characteristic of the language is the strongest draw card for me and I think that it is the foundation on which everything else rests. In this respect, Elm is in a class of it's own.

_Aside: When triaging bugs, the vast majority can be logically reasoned about quickly ( within a minute ). The fact that functions are pure, state is immutable and ADTs guard function scope means we can pinpoint the exact one or two places where a bug could occur, discuss implications of fixes and estimate/delegate the work on the spot rather than saying, "oh, lets reproduce it, investigate where it's coming from and _then_ make a informed decision". Right now we have 11 trivial logic bugs in the whole frontend. That's not bad for 50k LoC I'd say._

#### Responding to business needs, re-designs and regression

We move a lot of code, frequently. Every other week, there would be some sort of refactoring that touches 20-30+ files, makes core changes. The regressions have always been manageable and we've never shied away from doing this because of the fact that we encode so much into our types and so the compiler picks up all the things that we miss during a change. So each time, we opt to not carry technical debt because it actually makes more business sense to do it properly rather that put in a workaround in fear of touching a core system.

On the other hand, feature requests quite often ends up changing a type, which cascades to all affected functions. These end up being large changes. However, this is actually a good thing because the compiler is picking up every possible scenario known to the data types and making sure the modified type or state still runs 'correctly'.

So whilst the effort for each modification may mean a slightly higher upfront cost, it's actually saving us much more effort which we'd have otherwise spent down the line. Each of those `case ... of` or inference error the compiler warns us about is in fact saving our QA team and our customers hours of pain and frustration.

#### Hiring

This has been a tough one for us. Speaking franky but without saying too much, there is not a large pool of potential candidates for Elm in Sydney. However the _quality_ of candidates seems to be higher so we've been fortunate enough to fill our current needs. (I've only been involved in hiring for one other company so take my words with a grain of salt).


#### Community

Elm has a absolutely delightful community[^3]. It has grown considerably ( slack users ) since I joined two years ago and there is a tireless group of very helpful people always willing to help solve your problem. People there are so helpful they are _excessively_ helpful at times! I have learned so much about functional programming, game development and how to structure code just by asking questions, reading and having discussions with the knowledgeable people there. As a source of technical help, this is a invaluable resource to have.


#### So...

I hope this has been an informative read. I'm by no means an expert on Elm or SPAs, but the lack of these kind of long form technical articles is really what drove me to write one. It would be great for more people to shared their technical challenges and discuss their Elm projects in detail.

Elm 0.19 will come when it does, it seems to concern me far less than some on various social media channels.
But then again, those that are happily using Elm typically don't go shouting about it to the community.
Am I excited? Hell yeah! But until then, our team is really happy with how 0.18 is allowing us to rebuild a complex health insurance application at this pace with no compromise on quality.
And more importantly, it has really felt awesome all the way (forms was an exception).

At the current stage of the project, I'm really happy and comfortable with the team and codebase. We have a handful of bugs and the future is looking great... except for forms. I'll revisit that one when I've mustered a bit more IQ.

Oh and did I mention forms... ^_^

#### Footnotes


[^1]: Convoluted react-dnd issue, problem could very much be between the chair and keyboard - https://github.com/react-dnd/react-dnd/issues/429
[^2]: Drag and Drop for Castle of the Winds - https://github.com/mordrax/cotwelm/blob/master/src/Utils/DragDrop.elm
[^3]: Elm slack, come say hi if you haven't already - https://elmlang.herokuapp.com/