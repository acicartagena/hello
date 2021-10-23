---
layout: post
title:  Thoughts on Code Reviews
description: Fundamental flaws feedback, compassionate code review and other thoughts that help me when doing code reviews
date:   2021-10-22 20:12:35 +1000
image:  '/images/posts/code-reviews.png'
tags:   [code reviews, software development]
---

When reviewing code, I used to think it had to be something I 100% agree with.  I thought I was doing right, making sure any code that gets merged is as good as it can be. Looking back, acting as a custodian of the codebase, I was walking the line between that and gatekeeping. Back then, I was all about code consistency and maintainability, and I thought frustrating code review experiences were a trade-off to ensure a consistent codebase. Don't get me wrong. Code consistency and maintainability are essential. But focusing too much on the current way we're doing things, we might miss out on improving things for the better. 

### "Not the best choice" versus fundamental flaws feedback ###
New ideas or new ways of doing things are introduced in a code base and communicated via code review. Regardless of whether or not this is a good way to introduce changes (especially when working as a team), it happens often as we all aim to make code better. When trying to find the balance between maintaining consistency using existing patterns vs. exploring new ideas, I go back to this line from [this](https://blog.doist.com/decision-making-flat-organization/) article: Is this change something I can live with?

> Is this change something I can live with?

*"Not the best choice"* versus *fundamental flaws* feedback helps me figure out how much value I put in the changes I want to be done. *Not the best choice* means I can think of a better solution, but what's currently there is acceptable. The *fundamental flaws* feedback is where the current solution is unacceptable and being able to mention why concretely. There will always be different ways to solve one problem. The critical thing to keep in mind is that the solution doesn't always have to be how I thought. 

### Compassionate Code Review Comments ###
When it comes to actual code review comments, [this presentation](https://www.youtube.com/watch?v=Ea8EiIPZvh0) on compassionate code reviews is my go-to for more practical tips. It talks about three filters to use to check.  

 - Is it True?
    - if it's a fact (mention the source/additional documentation),  if it's opinion or a preference (say so explicitly), try a question and avoid "shoulds" or "right/wrong" language
 - Is it Necessary?
    - be aware of nitpicks, and check does it have to be addressed by this pull request
 - Is it Kind?
    - assume competence and seek to understand and remember you're dealing with a human with emotions

One of the more valuable tips is trying a question instead of telling the author what to do. A question can come in many forms. I initially took this advice and added, "can you do/change ___ ?". I was still telling the author what I wanted to be achieved and masked it with a question. And so sometimes I try to ask "what do you think of __ ?". This way we can have a discussion first, maybe they've thought about it tried it out and it didn't work or maybe this suggestion has inspired them and we can work on the solution together.

Over time, instead of making the author change their code, I moved to ask why the code was that way. From the answer I get, I could get more context as to their thinking and the requirement. Getting more context by asking why first has helped me weigh whether the changes I want to be done fit the problem being solved.

As part of dealing with humans with emotions, I'd also try to look for positive things or things I found to be good and make sure to let the author know by giving praise or a thumbs-up emoji. It might be considered noise by other people, but positive and negative feedback will help ensure good practices are communicated and maintained.

### Give more context ###
After figuring out what sort of code changes I think can make the code better, I try and sort out the reasoning why. When asking someone to change their current approach (something that works and is probably tested), I find it helps the suggestion whenever I give more context. The reasoning can give insight into my thought process and double-check my assumptions with my code review comment. If my goal is to teach a pattern or a principle, providing the reason also makes it easier for them to remember and adapt in the future.

Lastly, after explaining why, I also try and think if a code snippet or an example would help lessen misunderstanding. It provides something concrete that can be easily discussed. Sometimes describing changes or pseudocode can lead to assumptions being made and more back and forth if those assumptions aren't aligned. I also hope it shows that I (as a reviewer) have also made an effort to figure out if my suggestion would work with the current code being reviewed.

It might seem a lot of work to do all these when talking about code. (It's something that I try to be mindful of, and I don't always get it done) However, code reviews aren't like coding (where we're communicating with a computer, and it's primarily black or white or right or wrong). Code reviews communicate with a human (with emotions and ego) and deal with shades of gray. The outcome or the code changes might be the same, but the experience or how you get there with the discussion will be different. Over time, a collection of less frustrating code reviews is better for the people working on the same codebase.  
   
### What I Read (or Watched) ###
- [Compassionate Yet Candid Code Reviews](https://www.youtube.com/watch?v=Ea8EiIPZvh0) by April Wensel 
  - 25 minute video on the 3 filters to ask for compassionate code reviews
- [How to Do Code Reviews Like a Human (Part Two](https://mtlynch.io/human-code-reviews-2/)
  - Provides a familiar example of a bad code review
  - Offers up tips like bringing code up by a letter grade (from C to B), respect the scope of the review
- [Babylon Health Etiquette on Code reviews](https://github.com/babylonhealth/ios-playbook/blob/master/Etiquette/CODE_REVIEW.md)
  - Has good bullet points for everyone, for code reviewers and code authors
- [Code Review Guidelines for Humans](https://phauer.com/2018/code-review-guidelines/) by Philipp Hauer
  - Bit of a longer read, but it does provide good explanations for the different points made. It also has examples
  - There's also a "cheat sheet" similar to Babylon health's bullet points at the bottom of the article
- Google Engineering Practices
  - [The standard of code review](https://google.github.io/eng-practices/review/reviewer/standard.html)
    - Goal of new code is to improve the overall health of the codebase, code being reviewed doesn't have to be perfect
  - [How to write code review comments](https://google.github.io/eng-practices/review/reviewer/comments.html)
  - [Handling pushback in code reviews](https://google.github.io/eng-practices/review/reviewer/pushback.html) 

(Hello, I would be really grateful to get some comments/suggestions/feedback about this post. You can email me at hello@aci.codes or find me on Twitter @acicartagena)