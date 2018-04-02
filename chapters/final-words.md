# Final words

_Two months since starting this "blog post", we are on the cusp of 0.19, approaching 50k LoC and is almost, __almost!__, feature complete for our final major milestone which will coincide with our launch. I reflect on the last 10 months of development and talk about what I think are the strengths and weaknesses of working in Elm professionally._

So, what was originally just a blog post, has definitely turned out a fair bit longer than I had expected. Yet I still feel like I hadn't covered everything, such as page loading and routing, boilerplate state wiring ( especially for UI components ), the tendency for business logic to be 'lost' in functions in different modules, collaborating on a Elm codebase when major refactors are happening, testing, regressions and the list will probably go on for a while.
Hopefully what I have written will give those starting out a better idea of what to expect.


#### Not a framework

Elm is not a framework. It's not a library. It's a language. Beyond the basic necessities like url parsing and rendering to html, you're on your own. The ecosystem is young and libraries are sparse.

This is both a boon and a curse. It takes time to create all the bits and pieces of a SPA, the libraries that we create are not as battle tested and their APIs are probably bloated and coupled to our architecture. However, we build exactly what we need, when we need it and as new needs arise, we can confidently add the features required.

Overall, the language is so strong, it trumps not having ten alternative packages vying for your attention. Also, it would be unfair not to mention the packages that we do use, they are all solid.

_Aside: When I was making a game using React with react-dnd for drag and drop behaviour, I had frustratingly sunk days into trying to figure out some convoluted error message[^1] . When I was investigating Elm, I didn't find a drag and drop library so I built one, modeled after react-dnd. It has been working fine with no maintenance ever since. That was two weeks into Elm and took me a weekend to write._


#### Purity, Immutability, ADTs, Compiler ( Elm's quiet heroes )


_No runtime errors!_ is Elm's loud hawker. It boasts: 'come look at this, it runs without errors!'. Runtime errors are but a class of errors unfortunately made popular by dynamic languages and those that deal with lower level access. They need not exist.

How about logic errors? Errors in your runtime state? These are not picked up by the runtime but by a human when using your product. I'm talking about things like when you click a link but forgot to implement the route, scrolling through a carousel and it goes beyond the last item in the collection. Unit/Component tests you say? Sure. How about getting it right from the start, making it impossible to get into thees states.

What the hawker doesn't tell you is that Elm will _also reduce errors in your state to almost nothing if you want it to_. And by doing so, expose the only class of errors that we actually care about, domain logic errors. These are the ones where you call the delete endpoint instead of the create.

Purity, Immutability, ADTs and what the elm compiler does


#### Regression


[^1]: Convoluted react-dnd issue, problem could very much be between the chair and keyboard - https://github.com/react-dnd/react-dnd/issues/429