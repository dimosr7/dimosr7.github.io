---
layout: post
title: "How to bootstrap TDD in your team"
date: 2017-04-17
excerpt: "A way to introduce gradually TDD in the workflow of your team"
tags: [software, testing, tdd, test, driven, development]
---
Test-Driven Development (aka TDD) is currently one of the biggest buzzwords in the software industry. As a result, there are many misunderstandings around it. I am myself a "buzzword" person, so I remember experimenting with TDD some years ago, having so many questions. Having seen how TDD is claimed to be (but not has not actually been) embraced across the industry, I decided to write this post to provide a pragmatic approach on how teams can gradually embrace TDD.

The biggest myth around TDD (especially adopted by people new to the field) is that "**TDD is hard and it requires advanced cognitive skills**". This myth is busted if one looks into the root rationale behind TDD, which is to **empower developers so that they can develop software faster, more easily and with less bugs**. People think that in order to apply TDD, one has to be so clever as to be able to know in advance everything he/she needs to implement, write all the tests in advance and then proceed with the actual code. No! If anything, TDD's efficacy is based on small software development steps coupled with small feedback loops, helping the developer staying focused on a very specific piece of functionality <sup>[1]</sup>. If you think about it, TDD aims to make software development as dumb a process as possible! The size of these steps (and the corresponding feedback loops) is selected by each developer depending on his/her experience and comfort. However, having said that, TDD still requires a different mindset, which differs a lot from the common "test-last" (or worse "no-test") software development process. This means that it's difficult for a team to switch to TDD instantaneously. I have also experienced its steep learning curve in the past, so I will provide some interim stages that can be used from software development teams with the final aim to fully embrace TDD. These stages can help the team familiarise with the process and feel at ease, while also realising first hand its benefits. 

## Write one "function" at a time

In most of the teams I've worked or talked with in the past, developers have the following workflow: implement the whole class/component (whatever is part of the task) and then write all the unit tests for this component. Note here that since all the functionality is implemented, many developers use code coverage metrics to judge if they have tested enough so far. This is a big trap sometimes, because the fact that every single line is executed by our tests does not necessarily mean that all the code paths have been exercised. As a result, there might be bugs creeping in our code (and yes, being part of these teams I have also been a victim of this process). As a result, the first stage to depart from this is to start forming these small steps we mentioned before. Instead of implementing the whole functionality and writing all the unit tests in the end, a first significant change is to start writing each individual piece of functionality and then writing the unit tests for this part before proceeding with the next piece of functionality. This will help the developers get accustomed with shorter software development steps, which is one of the cornerstones of TDD. 

## Write a "dumb" version, write the test, refactor it

This stage is a slight adaptation of the actual [RED-GREEN-REFACTOR](http://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html) cycle of TDD. Conceptually, you will move the test step (RED) in the middle of the cycle. To elaborate further, the aim is for the developer to write the dumbest possible version of the required functionality (not caring at all about complexity, clean code etc.). Then, the developer writes a unit test to guarantee that the functionality is working as expected. In the end, having the existing unit test act as a safety net, the developer proceeds with the necessary refactoring of the functionality, to bring it into its final form. At this stage, most developers will hesitate a bit and ask the following question: "But, why delay something that will be done eventually, why not write the final version in the first place ?". I believe that this question is one of the first reactions to the different mindset required by TDD. Once resolved, a developer can realise that what's initially seen as a burden of TDD is actually a boost in the long term. So, the answer to the question is that writing the final version is expected to be much faster, because you will now have the unit test handy, so that at each refactoring you will be able to execute the unit test and verify that the functionality is the same (remember the small steps / small feedback loops mantra ?). So, TDD's claim is that the code required to (write a "dumb" version + write test + refactor/write final version) will be much less than the time required to (write directly the final version + write test). The only way to solve this paradox is to experience it on your own.

## Write a "pseudo-test", write a "dumb" version, complete the test, refactor it

This step is an even closer simulation to TDD and can potentially help you get the major benefits of it. Before start writing code, you will write a test that will exercise the specific part of code you plan on writing. However, since you still think that it's complex and time-consuming to write a full-blown test beforehand, you will do a part of it. So, you will attempt to write a "pseudo"-test (as I call it) in the sense that you will write all the parts of the test, setting up the dependencies and the SUT, setting the expectations, exercising the SUT, verifying results and interactions. But, you will write everything in a pseudo-language (something that is easily readable to you, even plain English!). As a result, the test won't be compilable, so you will have to comment it out. You will then write your code and then you will come back to translate your test in the language you are working on. There is a difference between this step and TDD, since in TDD the test has to be fully compilable (but still failing) before you write the code. As a result, in this step you will still use a form of test-driven development (but still not test-first), so you will benefit from the design feedback on your code before you write it. However, you won't be able to benefit from the green-red feedback cycle, since you won't have a working, failing test. Be very careful, because this step has a caveat: there is no step in this process, where you will have a failing test, thus you might write the test incorrectly in the first place and never catch that. To eliminate this risk, after writing the code, you can disable a specific part of the functionality (by commenting it out) and re-trying the test, which should now fail. Anyway, you don't want to have tests that can't fail, right ?

## Use full TDD for regression bugs

There comes a time when a new bug is filed for the team's code and a developer is assigned to fix it. This is one of the best spots to experiment with the actual TDD cycle and feel the thrill. The developer has a description of an existing bug in the codebase. So, the very first step should be to write a unit test that's failing, exposing this bug. Then, the developer can adjust the existing code, so that the unit test can successfully pass. Last but not least, the developer can also perform any refactoring, if the existing code can still be improved. Done. Yes, the developer has applied the actual **RED-GREEN-REFACTOR cycle** of TDD!

## Final stage

At this point, the developers of the team have made use of the 2 main pieces of TDD:
* working in small steps
* writing a test before writing the corresponding functionality

Now the only thing that remains is slightly reversing the second stage's cycle and following the RED-GREEN-REFACTOR cycle consistently. Well, have in mind that the team can still keep using TDD and non-full TDD way of work for a period of time, until the developers feel fully comfortable. 

From my personal experience, TDD is quite easy to follow when implementing components with a few dependencies and a significant part of functionality, but can be much harder when implementing components with a lot of dependencies and less actual functionality. For a more elaborate analysis on this point, you can read [this article](http://blog.stevensanderson.com/2009/11/04/selective-unit-testing-costs-and-benefits/).

### References:
[1] "Test Driven Development: By Example", Kent Beck