---
layout: post
title: "Beijing, a retrospective"
date: "2015-12-17"
---

#History
In October 2014 I was contacted by Publishing Technology to discuss the role of Chinese liaison, based upon my linkedIn profile stating web development and Mandarin Chinese experience. This was the first time someone other than a recruiter had made contact so although I didn't feel the role suited I humored them and we had several phone conversations.
03 March 2015
First day of work, first impressions; cubicles, dry air, cold, low desks, old chairs. Rough objective is to innovate, improve current technical tooling and methods. Spent most of my time in IntelliJ IDEA trying to build a basic java website with a login, evaluating the newest methods I can find. Gradle, Spring Boot, Java 8. Five weeks in, I begin working at home.

#personal goals
Improve my Chinese in a working environment.

#goals
Develop a dual language version of scitation.aip.org
Develop a framework to support the team to learn and work.
Assist the CTO with suggestions for process and organisational improvement.
Provide a direction for innovation.


#challenges
My experience limited to C#
Team experience limited to Java
My limited mandarin ability
One team member has C# experience but only WebForms
One team member capable of translation
First client still consuming majority or resource
One piece of test data, 300,000 expected


#results
1. feasibility
    It was made clear that choosing a language and framework the team were not familiar with would not be trivial. Leaving the path of least resistance to choose Java. I spent 3-4 weeks attempting to build a Java project with the same features as the blank ASP.NET MVC project. Just a login and bootstrap. I tried first to use nothing but the latest tools, Java 8, spring boot, Thymeleaf, continuing to follow the path of least resistance. Until after 3 weeks of banging my head against a wall day and night. I demonstrated what I had built so far, and I was embarrassed. I could even get the logged in user to display in the sidebar. I'd tried 3 different template engines, Thymeleaf, Freemarker, Velocity. To no avail. I decided to ask for help, help was not overly forthcoming and all seemed hopeless. I retreated to the soothing familiarity of C# and in a tiny fraction of the time had a framework which already had all the boilerplate I had worked so hard to build with Java over weeks. In a few hours I had language switching working and easy to use. None of the encoding fuss which some of the other Java projects where engaged in. I demonstrated this to my boss and colleagues and proposed we use C#. Suggested I could teach them, I had the ability to create a rapid learning environment. This would have been a wise choice if the boss had known what could be done. However communication was not ideal and from his perspective it was mearly a matter of cost, C# developers were sought out by the finance sector and as such came at a higher price than their Java equivalents. It seemed I had lost this fight, and would have to conceed to following the lead of my teammates in the initial design of the framework. At this point I was feeling a sense of impending crisis. My choices seemed to be build most of it yourself or build none of it yourself. During my Java research I had stumble on many different emerging frameworks like Angular, Hipster, Flask. Thankfully during the phase of the project where it was expected of myself and the team to create database and system design documents, I stumbled upon an article on the rise of javascript frameworks. It was then I discovered meteor a collection of contemporary tools and ideas which didn't ask you to learn 10 more paradigms, but instead held your hand and took all the buzzwords away. After this realisation, I was aware that I wasn't going to be easy to convince my bosses that it was a good choice. I had to manage all the risks. Luckily my whole team were wasting time writing meaningless design documents so I could focus on researching what we could and couldn't do.
2. Choice of tools
    There was a feeling of fight or flight going on for me and I wasn't ready to give up. I spent the coming weeks, working all day everyday considering everything my team mates and boss might be concerned about. Researching potential solutions for each as it came to me. Thanks to the package ecosystem behind meteor, much of this research was not focused on the subsystem tooling for aspects like pdf generation or xml parsing. My primary goal was to create some basic forms with fluent validation using the minimum code necessary. This would enable my team to pick up and learn the framework and by themselves build on it.
    Within the first month of tasks, my mind was abuzz with risks to manage and research to do. The most important and frustrating being the data import mechanism. I had two options, use xslt to parse the xml to html, and objects or manually write the parser. During the first few days of this I had the opportunity to see how nodejs packages could be wrapped in atmospherejs packages, allowing my contribution to be shared with the world. Quite an encouraging feeling. After this is became apparent anything written in nodejs was available to us in meteor. Many of the huge risks coming up in the final few releases seemed much less important after this realisation. As a result we have folded zip, pdf, excel, and xml manipulation into our web application.
    During the initial phase of the project I also stumbled upon docker, a tool which would cost a couple of us a lot of time, but was certainly worth it.
3. Communication
    Although at first this was the biggest problem it quickly became apparent my Chinese ability was not going to be the bottleneck to our project performance. The culprits of performance issues were largely due to the ideals of the client and the support team. Neither felt any reason to buy into agile development or learn about it, which meant working against the grain for our team.
4. Meteor
    Great web framework and really fast to work with. But in hindsight I was gambling on being able to introduce TDD after a month or two. This gamble didn't pay off and testing is still non-trivial, but the risk was mitigated somewhat by the simplicity of the framework. Due to most of the labourious form handling, validation and such being handled by packages and config there isn't a great deal to test. Most of the logic is in server side components such as the data import.
    > Unit testing in Meteor is non-trivial. The framework did not take into account unit testing from the outset and as such, it's hard to isolate units of code without fully loading the Meteor context, or a stubbed version of it. Perhaps when Meteor supports modules it will become easier to do this, but right now it's non-trivial.


Velocity Retrospective
History

Velocity was born in April 2014 as a result of a meeting between the major testing framework authors, each of which had their own role in the Meteor testing story. When we all came together, we proposed the following goals for a unified testing framework:

Simple installation
Flexible for the community to evolve
An easy Meteor-like workflow
A one-stop-shop for all Meteor testing

In July of the same year, it was endorsed by the MDG as the "Official Testing Framework" for Meteor. Fueled by the challenge and responsibility of this undertaking, we set out to create the Meteor testing solution to rule them all. The team included Mike Risse (mike:mocha) and Jonas Aschenbrenner (sanjo:jasmine). Let look at each goal above:
1. Simple installation

It's really easy to install Velocity-based frameworks. You type meteor add sanjo:jasmine or meteor add xolvio:cucumber and you're good to go. Some frameworks chose not to follow this ethos, but most did and there have been little to no complaints in this area.

Success.
2. Flexible for the community to evolve

Velocity was built from the ground up as a set of APIs that framework authors can use to build any testing framework or plugin. There are 6 testing frameworks on the Velocity homepage, and we are still seeing people extend and use Velocity in their own applications and packages.

Success.
3. An easy Meteor-like workflow

Velocity-based frameworks integrate nicely into the Meteor workflow. You can reactively see test results inside your app as you develop. The experience is far from perfect and can certainly do with the simplifying and streamlining love the MDG announced. More on this below in the test environments section.

Success... needs love.
4. A one-stop-shop for all Meteor testing

This was arguably the reason that the Velocity team got together; to unify our efforts as test-framework authors and combine our brains and smarts to create a one-stop-shop for Meteor developers. Today we still have a lot of confusion when it comes to testing with Meteor.

Learning: The MDG needs to express an opinion on how testing should be done with Meteor.
Velocity's Triumphs

In figuring out how to test Meteor applications, we needed to figure out how test all 7 testing modes of Meteor (see this blog post). This journey led to the following outcomes:
Package Testing using Jasmine / Mocha

Mike was doing some work for the Respond.ly team and figured out the pathway to using Mocha to run Meteor package tests. Soon after, Jonas generalized the solution and now you can use both of these fully-features industry standard frameworks to write package tests, instead of the primitive TinyTest.
App-level Client / Server Integration Testing

Both Jasmine and Mocha allow you to run tests within your running app's Meteor context. Whilst the package testing approach provided by TinyTest / SpaceJam / Mocha / Jasmine above provides you this in a package, it forces you to split your application up into packages in order for your application to be testable. This is not a reasonable ask as the package-only architecture is just one way to build apps.
App-level Client / Server Unit Testing

Sanjo went further with Jasmine and supported unit-testing modes. These tests run at hyper-speed and run without the Meteor context (they still need the Meteor to be running to establish a context. See more about this in the challenges section below).
App-level End-to-End testing

The nature of end-to-end testing frameworks is to run outside the context of the system under test, however running end-to-end tests reactively within the developer workflow gave rise to the @focus tag in xolvio:cucumber, which makes outside-in testing a lot smoother. Also, end-to-end applications need fixtures to setup data, and from this need the fixture-package pattern was created for sharing test-data setup code between integration testing frameworks and end-to-end frameworks.
Changes to the Meteor Core

In Q4 of 2014, the MDG added the debugOnly only flag as a result of a meeting between us all, this flag is used to keep applications out of production builds. This has enabld other development-only tools to be possible, such as the infamous Meteor Toys.

Not too long after that, Meteor supported the --test command to run Velocity-based framework tests. This runner can be seen here.
Incredible Uptake

At the time of writing this post, there are nearly 320k downloads of Velocity-based testing frameworks on Atmosphere.
Velocity's Challenges

To make the above happen, a lot magic was needed. Here are the issues that we have not been able to resolve:
Test Environments (AKA Mirrors)

This has been one of the toughest challenges for us.

When developing a Meteor application, the developer workflow is to start Meteor and start coding. To run tests reactively at the same time as building an app, we need to make sure the tests do not overwrite the main application data. For this to happen, the tests run inside a mirror, which is another word for a test environment.

In fact, this is how the TinyTest package testing mode works, it loads the packages and test files that you specify in the onTest section and provides you with an integration context, separate to your main application. Mirrors do the same, but they include the entire application context.

Our first approach to mirrors was called an rsync-mirror. This mirror used rsync to create a replica of the main app on the filesystem, and a second Meteor process was started on another port using the copied filesystem. This was great for doing things like instrumenting files and adding custom files/packages for testing, but the experience was not responsive enough, especially when the user would save files quickly (amongst a ton of other issues). So we scrapped it.

Our second approach was called a soft-mirror. It would wait for the Meteor build system to complete and then kick off a node process on the main.js file. This version would start within 30ms after Meteor started. We thought we hit jackpot! Unfortunately, it was not easy to load additional files that were needed for testing inside the test environment. So we created a test-proxy package. This package would scan the filesystem and add test files to the mirror only. Whilst the speed was amazing, the test-proxy approach was ridden with start/restart bugs, so we scrapped it.

Our third (and current) approach was to fork Meteor itself and modify it to make it support testing. It allows us to specify additional source locations and build file output directories. This approach has proven to be the most stable but it's still not perfect. The startup time of Meteor has been getting slower of late and with every release, we have to update a new Meteor track.

The first and third approach are both flawed in their need to run multiple build processes. This is where most of the CPU cycles get eaten up, along with the memory requirements becomin huge. When you consider that a lot of people use 3 mirrors, that's 4 Meteor apps running in parallel - a lot even for a mighty machine.

The reason Velocity is slow is due to mirrors.

What we really need, is the best of all the above approaches. A test environment where we can:

Load the test files we want into it
Specify the packages we want to include / exclude
Starts in milliseconds and in tandem with the Meteor lifecycle
The ability to instrument files (not essential but highly desirable for test coverage reports)

Deep Coupling

Unit testing in Meteor is non-trivial. The framework did not take into account unit testing from the outset and as such, it's hard to isolate units of code without fully loading the Meteor context, or a stubbed version of it. Perhaps when Meteor supports modules it will become easier to do this, but right now it's non-trivial.

This decoupling is what is needed for super-fast testing. Luckily, it is possible to achieve the same speed from integration tests using test doubles (like spies), but you still need to first start Meteor in order to get the context.

It would be amazing if the MDG did released an official Meteor stub with every Meteor release. The packages that your app needs may also need to be stubbed, but that's not nearly as difficult as most packages tend to export a single namespace and it's fairly easy to create test doubles.
Closing Thoughts

We have really enjoyed carving out the Meteor testing landscape and are proud of all the triumphs and to have persisted through the challenges.

We send the MDG our best wishes and look forward to seeing how they march forward with Meteor testing from here.
