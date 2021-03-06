---
title: "Microservices and ETL"
last_modified_at: 2020-05-14
categories:
  - architecture
tags:
  - architecture
  - microservices
  - ETL
  - data API
  - analytics
  - data swamp
  - data lake
  - DDD
excerpt: |
  Traditional ETL is an anti-pattern when it comes to decoupling. What are alternatives
  to ETL and how do microservices approach this problem?
---

TL;DR:
- ETL jobs are difficult to maintain middleware that deeply couples data sources with data consumers.
- Data APIs address the middleware and maintenance issues of ETL jobs, but still couple systems and can run into scalability issues that are poorly solved by API Management.
- By following a microservices approach, data is published with domain-defined events, addressing issues of coupling and scale; this approach applies equally well to systems integration as it does analytics.

## Problems with ETL
Extract, Transform, Load. [ETL](https://en.wikipedia.org/wiki/Extract,_transform,_load) refers to a long-standing practice of pulling data out of one system, transforming it (either through reshaping the data, annotating it, or both) and loading it for use by another system. It is a practice supported by a plethora of robust tools. With concepts like big data and data lakes prioritizing the capture of “raw data” ETL has sometimes become ELT (just extract and load the data and I’ll transform it later), but fundamentally _ETL/ELT is an integration pattern rooted in a highly coupled, monolithic architecture_. Data is at the heart of all systems, and by extracting data from one for the purpose of loading it into another, you are effectively binding those systems together at their very core. From that point forward, many changes in one system necessitate changes in others. The fact that the systems you’re loading to may be reports or analytics tools doesn’t change this – if the system changes, the report (and the ETL job) breaks, and you end up having to cascade your changes across the entire landscape.

Another big problem with ETL is ownership – who owns it? The source system is having its data extracted and the responsible team can tell you what the data means, the target system knows that they need certain values in a certain format, but the piece in the middle can’t be owned by either team. It’s like a bilateral trade agreement – it’s the product of negotiation, and any breaking changes result in a trade dispute.

## Pros and Cons of Data APIs
Data APIs are a huge step in the right direction. Data APIs break ETL into two parts with clear ownership. The source system publishes an API (aka a contract) and is clearly responsible for maintaining that API. This also means the API publisher only shares data they are comfortable sharing and remove the implementation details they don’t want to maintain. Similarly, those that are consuming that API are responsible for the integrating it into their system and can choose what parts of the API they integrate with and only pull what they need.

Unfortunately, data APIs still require direct system-to-system coupling. The approach shies away from data replication and thereby reduces the system’s autonomy. Naively, it can also result in scalability issues where a call to System A results in a call to System B, to System N and then back again. Such limitations can be overcome with caching, buffering, etc. but those strategies are then the responsibility of each publisher and consumer to devise and implement. The API coupling also means it’s harder for other systems to satisfy the same contract should you want to retire a system down the load. Finally, it is not uncommon for an enterprise to have multiple systems that do the same thing (for example, having multiple CRM systems because of organizational boundaries or acquisitions). An API approach would necessitate each consumer integrate with the API of each publisher of a given domain entity.

[API Management](https://en.wikipedia.org/wiki/API_management) can help mitigate some of the downside here, but those who have worked with them know API Management solutions can get quickly get unwieldy. More importantly, API Management used this way lives in that middle space and, like the ETL job, struggles with issues of ownership. API Management works well as a thin layer of indirection for external consumers and applications, but I am cautious about using it for internal systems integration.

[GraphQL](https://graphql.org/) offers a well-defined means of exposing and querying data APIs, and like API management can provide a nice way of wrapping up the data from many systems while allowing the requester to influence the shape of the response. However, GraphQL doesn’t address the underlying issues of Data APIs and their deeper reach (where you aggregate multiple resources in a single request) can increase coupling and fragility in ways that aren’t obvious to the consumer.

## A Microservices Approach
Microservices take a different approach to ETL. Rather than the system-provided API being the contract, the contract becomes published events. The published events are domain-defined rather than system defined and reflect (in part or whole) the business’s understanding of a domain entity or aggregate. This means that if multiple systems manage the same entity type, they can publish using the same contract.

Rather than having to call a system’s published APIs, consumers process the events they are interested in. Typically, one published event has many consumers and publishers don’t need to scale to meet demand as the number of consumers increase. As consumers store the data they are interested in (either by saving a copy or integrating it into their own models), they can service requests without having to call out to the publishing systems. This dramatically increases the autonomy of the consuming service and supports scaling in a much more granular fashion. It also means that unlike the other approaches, the consumer is completely decoupled from the publisher.

An additional advantage is that integrating using events means the default integration pattern is real-time. It may still make sense for the source system to continue to publish events as a “nightly job” either because of the state of the system or the nature of the data, but transitioning from events sent every night to events sent during the day is seamless. The consumer is also free to manage the impact of this change, as events are queued (typically by the event platform such as Kafka or Event Hub) and can be pulled on a schedule the consumer dictates. In fact, it may be that most events are not being published in real-time, but the integration _pattern_ is the same regardless.

What most distinguishes a microservices approach, compared to ETL and Data API, is that the publishing data conforms to the domain, not the system, and that data is shared in a way, using published events, that decouples providers from consumers.

## What About Analytics?
Thus far we have focused on system integration patterns, but what about analytics? Frankly, I don’t see loading data for use by an analytics platform any differently than for systems integration. Binding analytical tools directly to the stores for different systems increases coupling and overall system fragility (i.e.: if you change the system you break the analytics). Naively ETLing (or ELTing) that data into a data lake means that all those ETL jobs need to be maintained along with data catalogs, and because you’re often getting a data dump (rather than data that conforms to a domain-defined entity contract), you’re having to catalog data values that may not make sense outside of the system they support. You might think it’s better to share the data “because it might be useful” but it rarely works out that way. More often it just creates a [data swamp](https://en.wikipedia.org/wiki/Data_lake) that undermines the purpose of having the lake in the first place.

Hydrating your lake with published, domain-defined events avoids this issue. First, the data available is domain-defined and therefore well understood. Second, you only consume data required to support your analytics, further reducing the maintenance burden. Finally, because you’re pulling from an event stream, you’re creating real-time analytics (or at least the analytics are as up to date as the publishers are able to support).

## Moving Forward
It might be tempting to revert to using ETLs or take half-steps with Data APIs because they are familiar. But as you move out of a monolithic legacy environment and into a decoupled, microservices one, driving an integration strategy based on domain-defined events is necessary to fully realize the benefits of the approach. An event-driven approach addresses the ownership and coupling issues of ETL because the system that owns the data is publishing the data. Events and microservices also address the issue with API-based systems as the consumers bind to the contract/event, not the individual publishers, making it easier for other systems to fulfill the same contract while also improving the autonomy and scalability of your services. Because events typically represent things as they happen, your integration scales seamlessly to support real-time scenarios.