---
layout: post
date: "2020-05-11"
title: "Microservices: A New Approach to Old Ideas"
category: architecture
tags: architecture microservices agile DDD
---

What I find so attractive about microservices is that they provide a way of realizing long-sought principles and practices of software development by using lightweight, but powerful tools. This grounding in widely accepted best practices without many of the compromises or heavy up-front investment, required by approaches of the past, means you can approach them incrementally and with confidence. “Betting” on microservices is very different than bets of the past like J2EE or [RUP](https://en.wikipedia.org/wiki/Rational_Unified_Process) (tool heavy, vendor defined) or [ESB](https://en.wikipedia.org/wiki/Enterprise_service_bus)s (product-bound). Betting on microservices is kind of like betting on building something the way you’ve always wanted to.

The following are some of the principles that microservices move us closer to realizing while building complex scalable solutions, often atop an existing technical landscape. 

## Any non-trivial program contains at least one bug – Anonymous
The corollary to this is then to reduce the number of potential bugs you increase the triviality of the program. While microservices are not trivial programs, the fact that they are autonomous and scoped to a bounded context within a domain means that they are more trivial than software that is either not autonomous (directly coupled to many systems) or not operating within a well-defined scope.

## Software architecture is those decisions which are both important and hard to change – Fowler
I love the definition of software architecture as decisions that are important and hard to change. The implication then is that when you create adaptable systems (i.e.: those that can be easily changed) you want to limit the number of architectural decisions. The overarching “architecture” of a microservices-driven system is very simple: clear contacts and simple messages atop which strategies and patterns are applied on an as-needed basis to model more complex processes.

The strategies and patterns used for complex processes are _local to the process_. For example, when we decide to use a [Routing Slip](https://www.enterpriseintegrationpatterns.com/patterns/messaging/RoutingTable.html) for a message that must follow a specific processing sequence, we’re not saying that all services must communicate using Routing Slips. We apply what we need to, when we need to, to the job at hand, and allow others the same freedom.

The autonomy of each microservice means that what architectural decisions you do make are _local to the service_. In systems with non-autonomous (interconnected) components, architectural decisions are very difficult because of the wide-ranging implications of those decisions – this also makes the decisions much more permanent. Because each microservice can have its own architecture, you can be much more brazen and opinionated (which generally leads to simpler software and less code), and if you get it wrong, the smaller scope of the service means you can change it much more easily. In fact, based on our definition of architecture (important _and_ hard to change), we aren’t making architectural decisions.

## Domain-Driven Design – Evans
I loved reading Domain-Driven Design: it was like when you read your first book about software patterns and you find out there are standard names and structures for what you’ve been doing all along. Domain-driven design is generally difficult, and becomes more difficult when you rely on complicated systems (like many out-of-the box enterprise products) that, more often than not, force you to use _their_ domain to describe _your_ business. Starting from this already imperfect match, business is constantly evolving, and rarely does the path of that evolution match the path of the systems you’ve integrated. As the gap between the system and the business increases, that’s when the real pain of these now “legacy” systems is felt. The software you’ve invested so much in to try to enable the business becomes widely viewed as an encumbrance. By contrast, domain-driven design is about starting with a domain that is defined by the business and evolving that domain as the business evolves, integrating systems only where and to the degree that it complements the business domain (and being able to drop them when it makes sense).

The _foundational principle_ of microservices is that they be domain defined, and what tooling exists is in direct support of being able to define the services quickly and easily in your domain language. As Evans states, “Domain-driven design is a difficult technical challenge that can pay off big, opening opportunities just when most software projects begin to ossify into legacy”. Microservices provide a well-defined means of addressing the technical challenges while delivering the benefits of domain-driven design.

## Inherently Agile
As an industry, we have become very adept at “doing agile” without “being agile”, meaning we follow some methodology and do stand-ups and have a backlog, but we produce processes and systems that are slow and resist change. There are many reasons for this, but microservices provide a way of realizing the promise of agile: to be able to move quickly and easily.

Because the scope of a microservice is defined as a bounded context within a business domain, the software team must include substantial business representation. Without the business, there is no domain to represent and the service has no purpose. As the microservice is clearly bounded, it can be typically be worked on by a small (5 person/2-pizza) team. As well defined microservices are autonomous, the team can truly own the service and make many of the decisions about how the service operates.

What I’ve laid out is at the very heart of agile: a small team with a clear sense of ownership and a clear purpose. It’s the conditions under which we can progress through the cycle of forming, storming, norming, performing. It’s what [Daniel Pink](https://en.wikipedia.org/wiki/Drive:_The_Surprising_Truth_About_What_Motivates_Us) defined as motivation: autonomy, mastery, purpose.

## Conclusion
“Microservices” is working its way through the hype-cycle like so many ideas that have come before it, but it’s important to recognize the pedigree of the foundational concepts. Microservices are just services: defined by the domain they serve, scoped to a bounded context within that domain, and autonomous. They are what we as software developers and engineers have been desperately trying to build our entire careers, and now the barrier to entry is sufficiently low that we might just get the chance.
