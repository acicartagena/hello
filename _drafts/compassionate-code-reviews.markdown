---
layout: post
title:  Compassionate Code Reviews
description: TLDR - On PRs ask is it true? is it honest? is it kind?. Provide as much context as possible
image:  '/images/posts/code-reviews.png'
tags:   [code reviews]
---
### TLDR: ###
- compassionate code review
- author PR guide
- reviewer PR guide
  
***
Notes

Compassionate code reviews
Is it true
 - fact vs opinion
 - avoid this is right/wrong language
 - try question
 - avoid should
  
Is it necessary
 - be careful with nitpicks
 - check motives

Is it kind
 - assume competence, seek to understand
 - you're dealing with a human
 - choose the right medium

Google standard of code review
The primary purpose of code review is to make sure that the overall code health of Google’s code base is improving over time.

First, developers must be able to make progress on their tasks. If you never submit an improvement to the codebase, then the codebase never improves. Also, if a reviewer makes it very difficult for any change to go in, then developers are disincentivized to make improvements in the future.

 reviewer has ownership and responsibility over the code they are reviewing. They want to ensure that the codebase stays consistent, maintainable

 In general, reviewers should favor approving a CL once it is in a state where it definitely improves the overall code health of the system being worked on, even if the CL isn’t perfect.

the reviewer should balance out the need to make forward progress compared to the importance of the changes they are suggesting. Instead of seeking perfection, what a reviewer should seek is continuous improvement.

Google review comments
One way to do this is to be sure that you are always making comments about the code and never making comments about the developer. 

Explain WHY
sometimes it’s appropriate to give a bit more explanation around your intent, the best practice you’re following, or how your suggestion improves code health.

Google handling pushback in code reviews
When a developer disagrees with your suggestion, first take a moment to consider if they are correct. Often, they are closer to the code than you are, and so they might really have a better insight about certain aspects of it.

In particular, when the reviewer believes their suggestion will improve code health, they should continue to advocate for the change, if they believe the resulting code quality improvement justifies the additional work requested. Improving code health tends to happen in small steps.

Cleaning It Up Later
it is usually best to insist that the developer clean up their CL now, before the code is in the codebase and “done.” Letting people “clean things up later” is a common way for codebases to degenerate.

 If the CL exposes surrounding problems and they can’t be addressed right now, the developer should file a bug for the cleanup and assign it to themselves so that it doesn’t get lost. They can optionally also write a TODO comment in the code that references the filed bug.

### References: ###
- [Compassionate Yet Candid Code Reviews by April Wensel](https://www.youtube.com/watch?v=Ea8EiIPZvh0)
- Google
    - [The standard of code review](https://google.github.io/eng-practices/review/reviewer/standard.html)
    - [How to write code review comments](https://google.github.io/eng-practices/review/reviewer/comments.html)
    - [Handling pushback in code reviews](https://google.github.io/eng-practices/review/reviewer/pushback.html) 
- https://www.michaelagreiler.com/respectful-constructive-code-review-feedback/
- https://phauer.com/2018/code-review-guidelines/
- https://dev.to/mateusz_janusz/how-to-do-code-reviews-and-keep-a-positive-relationship-with-your-colleagues-2161

- https://mtlynch.io/human-code-reviews-1/
- https://mtlynch.io/human-code-reviews-2/