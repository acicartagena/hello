---
layout: post
title:  Pragmatic Programmer & A Philosophy of Software Design
description: TL:DR - Learnings, tips and a few quotable quotes. Hello!, The goal of this post/presentation is to introduce concepts & tips from Pragmatic Programmer & A Philosophy of Software Design books. (slides @ the bottom of the page)
date:   2023-04-30 01:12:35 +1000
# image:  '/images/posts/pr-metrics.png'
tags:   [software development, book notes, pragmatic programmer, philosophy of software design, tldr]
---

> Every rule has its exception, every principle has its limit

**"It depends"**   
One thing to remember throughout this post (and maybe in your software development career) is that most of the time, the answer is "It depends" because depending on the context, the background, and the reason why, the principle or rule is not applicable, or it would result in a red flag when done too much or too little.

# A Philosophy of Software Design
John Ousterhout writes the book. I used the 2nd edition, published in 2019. This book provides guidelines and principles for creating high-quality, maintainable, and scalable software systems. The book also emphasizes the importance of simplicity, abstraction, and strategic design to minimize complexity and improve software development.

## Complexity
Complexity is anything related to the structure of the system that makes it **hard to understand** and **hard to modify**

### Symptoms of Complexity   
One of the things that I really liked from this book is how it defines symptoms of complexity. I sometimes struggled with putting into words the gut feel i have and this somehow helps.   

#### Change Amplification   
Change amplification is when simple change requires code modification in multiple places. The goal of a software design is to reduce the amount of code affected by design decision, and that design changes don't need too many code changes.   
![change amplification](/images/posts/change-amplification.gif){: width="300" height="150" style="display:block; margin-left:auto; margin-right:auto"}

for example: before refactoring colors to be more semantic, when designers said to change the shade of blue, we had to go thru and find that shade of blue everywhere in the code

#### Cognitive Load   
Cognitive load is how much a developer needs to know to complete a task. Can the system be structured so that callers of that piece of code don't have to worry.
![cognitive load](/images/posts/cognitive-load.png){: width="300" height="150" style="display:block; margin-left:auto; margin-right:auto"}

for example: api with too many methods, global variables, dependencies between modules sometimes an approach with more lines of code is actually simpler, because it reduces cognitive load

#### Unknown Unknowns
It’s not obvious which pieces of code must be modified to complete a task. Something a developer needs to know and there's no way to find out and the only way to be certain is to read every line. Another goal of a system is to be obvious. A developer can make a quick guess about what to do and be confident
![unknown unknowns](/images/posts/unknown-unknowns.gif){: width="300" height="150" style="display:block; margin-left:auto; margin-right:auto"}

### Causes of Complexity
**Dependency** - A piece of code can not be understood or modified in isolation. Dependency leads to Change Amplification and Cognitive Load. (Like meetings, I don't think we can fully not have any dependency on a complex system. The goal is to minimize dependencies, make it simple and obvious)

**Obscurity** - Important information is not obvious. One big culprit is inconsistency. Obscurity leads to Cognitive Load and Unknown Unknowns.   

The next sections are more to do with ideas / quotes on how to minimise complexity

> "Working Code isn't Enough"

![workaround](https://www.monkeyuser.com/assets/images/2018/88-workaround.png){: width="375" height="373" style="display:block; margin-left:auto; margin-right:auto"}

### Tactical Programming ❌
- Get something working
- May be a bit short-sighted
- Planning for the future isn't a priority

### Strategic Programming ✅
- Invest time to improve the design of the system
- Proactive investment
- Try a couple of alternative designs

(It doesn't have to be one or the other, I'm a believer of also trying to get things to work first, which is tactical programming, then look into ways to make it better, which is strategic programming)

> "Modules should be deep"

#### Modules
- Relatively independent software. Can be divided into **Interface** and **Implementation (Functionality)**   
For example: Functions, Classes, Subsystems or Sercices

#### Interface
- Describes what a module does and not how it does it
- Cost of using a module (What a developer needs to know)

### Deep Abstraction ✅ vs Shallow Abstraction ❌
![Deep vs Shallow](/images/posts/deep-vs-shallow2.png){: width="761" height="300" style="display:block; margin-left:auto; margin-right:auto"}

#### Deep Abstraction ✅ 
- More details abstracted from the Interface, the better
- Benefit of the module is its functionality 
- Cost of the module is it's functionality

#### Shallow Abstraction ❌
- relatively complex interface in comparison to the functionality it provides
- the benefit they provide (not having to learn how they work internally) is negated by the cost of learning & using their interfaces
- example: Pass Through Module ❌   
   - method offers no abstraction, since all of its functionality is visible through its interface   
``` 
private void addNullValueForAttribute(String attribute) {
    data.put(attribute, null);
}
```

![Deep vs Shallow](/images/posts/deep-vs-shallow.png){: width="400" height="400" style="display:block; margin-left:auto; margin-right:auto"}

### Combine vs Split methods
- Splitting methods introduces complexity
  - More components the harder it is to track and find
  - Additional interfaces to consider
  - Creating separation means the components may be farther apart
    - End up flipping back and forth to understand how they work
- example: Conjoined Methods ❌   
  - physically separated methods, but they can only be understood by looking at the other
  - ideally, methods should be understood independently

> "Design it Twice!"   

- Provide multiple options for **major** design decisions. Modules or components that have wide impact in the system or codebase
- Compare alternative designs. Consider the following factors:
  - Radically different approaches
  - Compare weaknesses vs features of designs
  - Does one alternative have a simpler interface?
  - Does one interface have a more efficient implementation?

> "Code should be Obvious"    

- Obvious code should allow a developer to read it quickly without much thought
  - and the first guesses and assumptions about the behaviour are right
- 2 factors to consider to help making code obvious:
  - **Consistency**
    - Similar things done in similar ways
    - Reader recognise patterns
      - Can draw safe conclusions without analysing the details 
  - **Obvious names**
    - names that are meaningful, provide clarity and reduce the need for documentation


> "Software design is never done. Experience shows better ways to do things

# Pragmatic Programmer
I first read this book from the advice of my mentor. For this, I used the 20th anniversary (2nd edition) published on 2019. The examples in the book may have aged, however I think the tips and the lessons can be considered timeless. This book was written by David Thomas and Andrew Hunt. I'd chosen to share 10 tips I found very useful in my day to day. 

## 1. Provide options, don't make excuses 🙀
- It is us up to us to provide solutions or alternatives, instead of making excuses like the cat 🙀 ate my source code
- Explain what can be done to salvage the situation
- Don't be afraid to to ask or admit we need help

> When you find yourself saying, “I don't know,” be sure to follow it up with “—but I'll find out.” 

## 2. Don't live with broken windows 🪟
- Broken windows 🪟 instills a sense of abandonement, that the owners of the building don't care
- Don’t leave “broken windows” (bad designs, wrong decision or poor code) unrepaired
  -  Broken windows doesn't need to get replaced, at the very least board it up or let others know about it and come up with a plan of action. This may be letting the team know about the broken window, or leaving a JIRA ticket or a comment on the PR
- Also, don't cause damage just because there's a crisis of some sort 👩‍🚒🔥
  - Remember the story of a very pristine, immaculate and clean house that caught on fire. The firefighters, with their expertise determined there's enough time to remove their boots so as not to dirty the house while fighting the fire. 
  - Aim to have a very clean, pristine codebase that no one wanted to be the first one to mess it up

## 3. Remember the big picture 🐸🫕🔥
- Constantly review what’s happening around you 
  - Not just what you’re doing
- Don’t be like the Boiling Frog 🐸🫕🔥
  - “They” say that if you take a frog and drop it into boiling water, it will jump straight back out again. However, if you place the frog in a pan of cold water, then gradually heat it, the frog won't notice the slow increase in temperature and will stay put until cooked.  
  - Science says ^ the above story is not true. But this makes it easier to remember tip 3

## 4. Good enough software
- Does **NOT** imply sloppy, hacky or poorly written code
- Users would rather use software with rough edges TODAY than wait months for shiny version
- Know when to stop
  - Don’t spoil a good enough code with OVERREFINEMENT
  - Move on, and let your code stand on its own right for a while

## 5. Invest regularly in your knowledge portfolio 📈📚
- The more technologies you are comfortable with, the better you will be able to adjust to change.
- Don’t put all your technical eggs in one basket
- Ideas / Suggestions:
  - Read technical & non technical books
  - Stay current - Read news and posts online on technology different from that of your current project
  - Learn a new language
  - Experiment with different environments

## 6. Critically analyse what you read and hear
- Get closer to the root cause
  - Ask the 5️⃣ Whys
![Why](/images/posts/pragmatic-why.gif){: width="300" height="150" style="display:block; margin-left:auto; margin-right:auto"}
- What’s the context?
  - Everything occurs in its own context
  - “one size fits all” solutions usually don't because it depends on the context
- When there's an article or book touting a “best practice”
  - Best for who?
  - What are the prerequisites?
  - What are the consequences, short and long term?
- Why is this a problem?
  -  Is there an underlying model?

> A good idea is an orphan without effective communication.
  
## 7. It’s both what you say and the way you say it
- Know your audience
  - Understand the needs, interests & capabilities of your audience
  - gather feedback. Don't just wait for questions: ask for them
  - Continuously improve your knowledge of your audience as you communicate.
- Choose your moment
  - Make what you're saying relevant in time, as well as in content. 
  - “Is this a good time to talk about...?'’ or "Do you have the headspace to talk about..."
- Be a Listener
  - Encourage people to talk by asking questions, or ask them to restate the discussion in their own words
- Get Back to People
  - In the rush of everyday life, it's easy to forget
  - Always respond to emails and ~voicemails~ slack, even if it's "I'll get back to you"

## 8. There are no final decisions
- The mistake lies in assuming that any decision is cast in stone and in not preparing for the contingencies that might arise
![Pivot](/images/posts/pragmatic-pivot.gif){: width="300" height="150" style="display:block; margin-left:auto; margin-right:auto"}
- Flexibility in the areas of architecture, deployment, and vendor integration.
- What you can do is make it easy to change
  - Hide third-party APIs behind your own abstraction layers. 
  - Break your code into components: even if you end up deploying them on a single massive server

### Reversibility
- There is always more than one way to implement something, and there is usually more than one vendor available to provide a third-party product.

> No one writes perfect software, so it's a given that debugging will take up a major portion of your day.

### Debugging Mindset
- You need to turn off many of the defenses you use each day to protect your ego, tune out any project pressures you may be under, and get yourself comfortable.
- Always try to discover the root cause of a problem, not just this particular appearance of it.
- When trying to solve any problem, you need to gather all the relevant data.
- Are there any other places in the code that may be susceptible to this same bug?
  - Make sure that whatever happened, you'll know if it happens again. 
- if the bug is the result of someone's wrong assumption, discuss the problem with the whole team

## 9a. Failing test before fixing code
- The best way to start fixing bug is to make it reproducible.
  - if you can't reproduce it, how will you know if it is ever fixed?
- isolate the circumstances that display the bug
  - you'll even gain an insight on how to fix it.  

## 9b. Don't Assume it - prove it
- Don't gloss over a routine or piece of code involved in the bug because you “know” it works.
- Prove it in this context, with this data, with these boundary conditions

## 9c. Read the error message
- In our panic, stress we might gloss over the error message. 

## 10. Avoid Fortune-Telling
- Don’t outrun your headlights 
  - We can't see too far ahead into the future, and the further off-axis you look, the darker it gets
- Design for future maintenance? Yes, but only to a point: only as far ahead as you can see.
- You might find yourself slipping into fortune telling when you have to
  - Estimate completion dates months in the future
  - Plan a design for future maintenance or extendability
  - Guess user's future needs
- The more you have to predict what the future will look like, the more risk you incur that you'll be wrong.
- Instead of wasting effort designing for an uncertain future, you can always fall back on designing your code to be replaceable.
- Much of the time, tomorrow looks a lot like today. But don't count on it  

# Presentation
<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vQaCBEtBfIbxfFKcsmDYL0toDeVMYpejEkw5sW8LPNt3NJ8Agguskxj8eRV7Bu3dsGiJ1NFf8X_2EiM/embed?start=false&loop=true&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>