---
layout: post
title: Notes on A Philosophy of Software Design
description: TL:DR Things I found interesting from Philosophy of Software Design
date:   2023-04-30 01:12:35 +1000
# image:  '/images/posts/pr-metrics.png'
tags:   [software development, book notes, philosophy of software design, tldr]
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

![workaround](/images/posts/workaround.png){: width="375" height="373" style="display:block; margin-left:auto; margin-right:auto"}

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