---
layout: post
date: "2020-05-22"
title: "What is a Microservice"
category: architecture
tags: architecture microservices DDD events messages product API data
---

There are many different definitions of a microservice out there. As more and more people enter the space and provide tools to support microservice development, the definition of a microservice only becomes more confusing (kind of like what happened with “devops”). When I write of microservices, I have a very specific definition in mind. Hopefully this post will help bring some clarity, at least within the context of this blog.

Microservice is a high-level pattern or *architectural style*. This architectural style has several key characteristics that both narrowly define what it is, while leaving room for a lot of flexibility in the implementation. Accordingly, using a specific tool such as containers or serverless has little to do with whether you are following the architectural style.

A microservice is defined as something that:
- satisfies the requirements of a bounded context in a domain
- can be maintained by a small (3-9 person/2-pizza) team
- is autonomous and owns its data exclusively
- communicates asynchronously using “dumb pipes”
- has an API

## Bounded Context

A microservice satisfies the requirements of a bounded context in a domain. Consequently, to build a microservice you must start with a solid understanding of your domain and the requirements of bounded context you are working to satisfy.

This is a significant paradigm shift for most IT organizations that are focused on supporting systems that support the business rather than supporting the business directly. This can also be a paradigm shift for the rest of the organization, where they have become accustom to defining their role as it relates to system capabilities rather than business needs. In fact, the idea of building components that are defined by the domain they operate in rather than the system they integrate with is so profound, it is often transformative. This transformation has two key dimensions:

- **Domain Driven**: If IT must now build something that satisfies the requirements of a bounded context within a domain, they need an intimate understanding of that domain. To effectively gain that understanding, business and IT need to operate as a single team and jointly define the domain and bounded context they are trying to support.

- **Product vs Project**: While systems are relatively static, business is constantly evolving. Since we are developing something that aligns with the business, it must too constantly evolve. What we are building can be best thought of as a product (rather than a project). Best practices for product development are agile practices, with frequent releases, a dynamic backlog of work, and no end-date (the product is never done as the business is always evolving). This is a profound shift for organizations accustom to delivering projects, which are characterized by fixed budgets, scope, and most significantly, a clear end-date.

Satisfying the requirements of a bounded context is typically not done by a putting all that functionality in a container, or an Azure Function or AWS Lambda project. In fact, a single microservice often involves serverless functions, containers, databases, and a variety of other tools. *The “micro” from microservice comes from constraining the scope to a single bounded context, but it’s not small*. If you are thinking of a microservice as “a function” or “less than 50 lines of code”, that is not what it means. A microservice is small relative to traditional enterprise systems like CRM and ERP software whose endpoints and integrations span many bounded contexts (ex: a single system that defines Product, Order, Customer, Sales, etc.)

## Small Team

A microservice can be maintained by a small team. The corollary here is that it requires a small team to maintain a microservice. This perspective can be helpful in framing the scope of a bounded context and the supporting microservice. As different parts of the business tend to evolve at different rates, it might be possible to have one team maintain 2-3 microservices, but not more than that.

Getting the domain right and defining your bounded contexts appropriately is critical here. I’ve [read articles](https://segment.com/blog/goodbye-microservices/) where relatively small teams are struggling to maintain hundreds or thousands of “microservices”. Having this many services is harmful and marks a departure from the architectural style. If your architecture includes 100 microservices, then you likely have 1,000-2,000 people developing those services. 1,000 microservices? That’s 10,000-20,000 people … in IT, building services.

There are very few businesses that operate in or across domains that would have 100 bounded contexts. In cases where the business is that large, there is a natural separation (divisions, lines of business, etc.) between domains that helps reduce complexity. 3-7 microservices/bounded contexts is a reasonable starting point.

## Owns Data

A microservice must be autonomous: it must be able to satisfy a request without having to interact with other systems or services. Once the request is satisfied, it is likely an event will be published that other services are interested in, but events should never travel between services as part of satisfying the request itself. This autonomy is critical for maintaining the scalability of the system and avoiding error-prone communication patterns (like retry events).

To achieve this autonomy, every microservice must own its own data. The scope of what data it needs to own/maintain is whatever is necessary to satisfy an incoming request. The most obvious consequence of this approach is a lot of data replication – if customer information is needed for sales, service, operations, etc., then each one of those services will have to store some customer data. Trust me, that’s okay.

I have seen many projects suffer, and especially service-oriented projects, because the services don’t own the data. At its worst, there is a “data service”, but more typically a database is shared between services. This makes the services impossible to isolate, difficult to test, and difficult to scale (since the data ends up being the bottleneck). Inevitably, the database becomes a back-channel communication mechanism that undermines the integrity of the events.

If a microservice does not own its data, it is not a microservice.

## Communicates with Events

Microservices communicate with each other using domain-defined messages. Because messages are domain-defined, they are expressed in the ubiquitous language of that domain and do not require any transformation.

The communication mechanism should be scalable, so it can support an increasing number of messages over time, and asynchronous, to allow for temporal decoupling between the services.

We want to stick to “dumb pipes” for a couple of reasons. First, the smart-pipe model, best characterized by an enterprise service bus (ESB), often becomes an architectural boat-anchor. ESBs were introduced as a compromise, where the best solution was to change the systems themselves so they could more easily integrate, but since the system was difficult/impossible to customize, the ESB did the heavy lifting. As the business continued to evolve, the number of system changes we wanted to make (but couldn’t) increased. The amount of functionality in the ESB grew over time, eventually becoming monolithic, brittle, and difficult to change in the same way the systems it was interfacing had.

The second reason for “dump pipes” is that it is important for those consuming the messages be able to accept the messages that are being published. Any manipulation we would do at the message layer would lack the rich context the publisher and consumers have, and it becomes something we need to maintain outside of the service (and therefore, the bounded context), increasing the fragility of the system and changing the contractual, message-based relationship between services. To the extent that buffering, retries, etc. are needed, they should be the responsibility of the consumer, who is often best able to implement these strategies, and not the messaging platform.

## Microservices have APIs

Microservices expose their functionality to non-microservices using APIs. If the application you are building needs Order information, it can call the Order microservice API. If it needs Customer information, you can call the Customer microservice API. Often you don’t want your applications interfacing with the services themselves, so a proxy or gateway might make sense, along with API Management.

## Summary

Microservices satisfy the requirements of a bounded context within a domain, can be maintained by a small team, is autonomous and owns its data, communicates asynchronously via dump-pipes using messages, and exposes an API. Anything less, and you are following a different architectural style to which the patterns and benefits may not apply.

Many issues others have faced with microservices come from a misunderstanding of the architectural style. Anti-patterns such as treating a microservice as any “small service”, integrating it with other services directly as opposed to with messages, sharing databases, or primarily modeling them after system functions rather than business domains result in the same challenges around scalability, maintainability, and legacy that microservices were intended to overcome.

Done properly, the benefits of using microservices are many. The freedom of the style and service autonomy means different services can be implemented in technology that best suites the requirements of the domain and update their technology independently. Service autonomy and asynchronous communication allow services to scale independently. Most importantly, managing your service development as a product, not a project, allows it to as the business evolves, realizing an evolutionary system and architecture that stays aligned to business needs.
