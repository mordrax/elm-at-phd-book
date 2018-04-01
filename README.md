# Introduction


_This is a story of a guy who left it all to chase Elm full time, the technical trials and tribulations he faced, the euphoric and … not so euphoric bits of writing a SPA in Elm. My scope is ambitious, use these italic summary headers to decide on the sections you want to read._

Total word count: around 13,000

Reading time: 65 minutes. + Code snippets

I write Elm at Pacific Health Dynamics, a small health insurance software vendor with big dreams. Since July 2017, I’ve been leading the frontend rewrite of their flagship product.
The codebase was at 16k LoC when I started. Since then, I’ve rewritten the various subsystems at least once (I'm looking at you _generic form component_). Now we hover around 45k LoC with most of the common SPA structures stabilizing. We are about a third of the way to completion. This is a typical massive, legacy, regulated system.

The driving motivation for this article is to share my experiences, discuss the various challenges we faced and provide practical solutions that we took to overcome them. I feel that there is not enough long form analysis from teams using Elm and that is something I'd craved when deciding whether to take on Elm in a professional setting rather than just as a hobby.[^1] Therefore, this article is aimed at those similar to where I was, not sure whether to take the step or for teams who are using Elm and struggle with the various topics I cover here. To that effect, the code samples here are not for beginners of the language and my focus is not in explaining basic concepts.

_Aside: Constructive feedback/discussions are very welcome. As I'm just learning this myself, please share any ideas or how your team may be doing somethings differently by hovering over a paragraph and commenting on it. Thanks._


# Overview

So, at its heart, this a story. And a story, always has a beginning ([Prologue](/chapters/prologue.md)).

The next chapter ([Brave new w..holy cow](/chapters/brave-new-world.md)) details my analysis of the existing codebase when I started.

From there, we go straight into strategies for [Refactoring](/chapters/refactoring.md) large codebases. Around that time, we started hitting brick walls re [Compile times](/chapters/compile-time.md) which (prodded by Noah) produced a talk at a Elm remote meetup[^2] with slides[^3].

With a much more structured foundation, I started developing patterns for [Child to parent](/chapters/child-to-parent.md) communication, our various types of [Components](/chapters/components.md) matured, and I tackled generic [Forms](/chapters/forms.md) over and over, which I'm still unhappy with.

A core piece of our frontend is how it interacts with the backend through our [Endpoints](/chapters/endpoints.md) which consist solely of auto-generated decoders. [Extensible types](/chapters/extensible-type-hell.md) are powerful but also fun!

I talk about our [File Structure](/chapters/file-structure.md), which grew organically. The major consideration here is compile time. And I throw together a bunch of random [Tools](/chapters/tools.md) which may be useful if you're making a SPA (useless if you're making a game).

Finally, I [rant and rave](/chapters/final-words.md) about how much I love Elm and try my best to word it like it's an objective observation of the strengths and weaknesses of the language.

# Thanks

To Julian Livingstone who was my mentor in Elm and gave his time freely to review and critique this article.
He's also a mad keen Haskeller. Check out his wonderful Haskell book: http://www.happylearnhaskelltutorial.com/

#### Footnotes

[^1]: Castle of the Winds remake in Elm - https://github.com/mordrax/cotwelm
[^2]: Elm Remote Meetup talk - https://youtu.be/ulrukPRYsws?t=50m4s
[^3]: Elm Remote Meetup slides - https://docs.google.com/presentation/d/10vN7eLr3qsd4nK2zcxUHgbu68fO_yzAA-b7Hf7kEcik/edit?usp=sharing