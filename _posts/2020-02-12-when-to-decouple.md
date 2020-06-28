---
title: "When to Decouple Systems"
last_modified_at: 2020-02-26
categories:
  - architecture
tags:
  - architecture
  - decoupling
  - microservices
  - transformation
excerpt: |
  Decoupling systems is a proven way to unlock value across a landscape of existing
  enterprise systems, but when does it make sense to invest in this approach?
---

Organizations have made huge investments in software and technology to stay
current and get ahead, but the pace of technology change, evolving customer
demands, and competitive pressure leaves them feeling encumbered by past
investments without a clear path forward. Keeping these existing systems up to
date can be difficult and expensive, often requiring large up-front investments
or costly upgrades that take months or years to roll out, by which point they’re
soon facing the next upgrade. Additionally, systems are often deeply integrated
with one another and taking on one system upgrade can feel like taking on
upgrading every system. Technology once seen as a critical business enabler is
now seen as baggage, slowing or preventing change necessary to keep the business
competitive. How can we move forward? How can we move forward quickly?

Decoupling works to incrementally add value (features) while embracing the
existing system landscape, but it’s not a silver bullet; it shouldn’t be used
for everything and comes with its own implications. In what follows we define
modern decoupling practices (“digital decoupling”), consider the alternatives,
and examine when to use it.

## What is Digital Decoupling?

Decoupling can mean different things to different people. For our purposes,
digital decoupling is creating lightweight, *domain-defined services*, often
supported by *existing systems*, that *share information*. By domain defined, we
mean services that reflect the ubiquitous language of the user whose
capabilities relate directly to their work or function. Having services be
defined by the domain they operate in rather than by the system they abstract is
critical to appropriately scope the service and prevent the underlying systems
from creeping into the domain.

The second part of our definition is that we embrace existing systems. In most
companies a system replacement is neither desired or feasible, and while it may
become feasible over time, we must start by embracing those systems if we are to
deliver value quickly and incrementally. By defining the work as what provides
value to the user (in the language of their domain), we can consider *small
parts* of *many systems* and scope down our decoupling efforts to the minimum
required. In this way technical debt and other encumbrances are tackled
piecemeal and on an as-needed basis.

Finally, one reason decoupling is considered in the first place is that the
system we have doesn’t do what we want but it *owns the data*. By sharing
information, we abstract the details of specific system-to-system integration
and enable all kinds of use-cases – particularly in the data and analytics
space.

### How Is it Done?

There are several ways to decouple systems, but a modern architectural approach
is to leverage a cloud-native architecture using micro-services and
message-based communication. It’s a PaaS-first approach: easy to provision, you
can start with as little as you need, and be confident in its ability to scale
and grow over time. Architectural decisions about how to decouple a specific system
are scoped to the microservices decoupling that system. The patterns for sharing
information out and between services are well-established and directly supported
by PaaS components.

Decoupling enables delivering value to the user incrementally. This implies an
*agile* way of working where the user is part of the team. There is no room for
“over-the-fence requirements” when you’re delivering every two weeks (or every
day, or every hour as many do). There is no room for “your department” and “my
department”. It’s collaborative.

### What are the Alternatives?

When facing a decision of when or where to do something, it’s important to
consider what the options are. In the case of decoupling, the options are to
largely to continue as is by:

- Investing in existing systems to extend their functionality to meet the
    changing needs to the user

- Buying new auxiliary systems and integrate them directly with existing
    systems and data (either as a new product or additional modules for existing
    products)

- Replace existing systems with new ones

Depending on your needs, the above strategies may be the right ones (and often
are). Furthermore, decoupling systems is fundamentally a software development
project and the build vs. buy decision is as relevant here as it would be with
any custom software project.

## Digital Decoupling is Custom Software Development

Digital decoupling *is* custom software development, with many of its
traditional implications. These implications should be considered when deciding
to embark on a digital decoupling journey.

### Traditional Concerns and Advantages of Software Development

Software development is expensive, and there will be some up-front costs in
establishing core patterns of microservices and data sharing, provisioning your
cloud PaaS components, etc.

Most significantly, shipping software is “the end of the beginning” rather than
the “beginning of the end” as it is with COTS (commercial off-the-shelf)
software deployment. As a team engaged to deliver value to users incrementally,
you should plan on some level of continuous investment to support the team and
the work. Consequently, it’s fair to have a sense of what the backlog will be
for the next several releases and a roadmap that extends for 6 to 12 months
before getting started. Rarely does a “one and done” project make a good
candidate for custom software development – you ship custom software to *learn*,
and the reason you go custom is because your business is unique and the scope
being considered is a differentiator.

### Additional Advantages

While digital decoupling requires custom software development, it has some
advantages compared to custom-built products of the past. A cloud-native,
PaaS-oriented architecture significantly lowers the barrier to entry on getting
started. This is effectively “commercial off-the-shelf infrastructure” that
takes a significant bite out of traditional start-up costs while providing
assurances around security and scalability. It is reasonable to expect results
in a “weeks-to-months” timeframe rather than the “months-years” timeframe
typical of both custom software development and large COTS software deployments.

Second, many projects of the past have been anchored around system replacement
or paying down technical debt. This approach embraces existing systems – in
fact, one of the first tasks when beginning a decoupling journey is to figure
out how to get at the data and establish a pattern for accessing and working
with existing systems. Furthermore, since the work is scoped to the domain and
user needs, the implementation is focused on a small part of an existing system
rather than taking on what would otherwise be an unwieldy integration project.

Finally, the top-level architecture is extremely lightweight and the
consequences of how a system gets decoupled are local to the service (or
services) decoupling it. This means it’s easy to experiment, to change and
refactor within a service than it would be if the services were larger and
integration were the focus. In theory every service or team could have its own
unique architecture, make different technology choices, etc. Of course, there
are some advantages to having a standard approach and there are benefits to
sharing best practices among teams, but the overall approach encourages making
the best *local* decision within a service. Local decisions avoid burning time
trying to come up with a more generalized approach/architecture, and
consistency/integration is achieved through the governance of the shared data
and inter-team contracts, rather than the means of integration.

## When to Decouple

When should you approach a problem using decoupling? It will depend on if you’ve
done it before (and if the architectural patterns are established), what the
alternatives are to deliver value, and the expected return on investment.

**Getting Started**: Your journey to decouple systems should not start with a
bang. The first decoupling effort should be small in scope, user-driven, and
stand on its own as a good investment decision. Ideally, this first initiative
will establish the behavioral and architectural patterns that can be held up as
an example for others to follow.

**Consider Alternatives**: If value to the user can be delivered with a simple
upgrade or configuration change within an existing system, then there is no
point in complicating things with the custom software and infrastructure to
decouple it. There are many great COTS software solutions that can and should
continue to fully and faithfully deliver the required value.

**Define Value**: Decoupling should never be done for decoupling’s sake. While
it might be tempting to imagine every system sharing every event and
notification in case it *might be useful*, the odds of you sharing the right
information and in the right way without a clear use-case are effectively zero.
Don’t do things because you feel it’s the right thing to do – prove that it’s
the right thing to do before you start by establishing an expected ROI.

### Strong Candidates for Decoupling

If the value to the user is well defined and supported, then decoupling is an
*alternative* to delivering that value some other way. In that context, the
following would be strong candidates for decoupling:

- When the alternative is a 6-to-24-month COTS migration, deployment or
    upgrade in a competitive area of the business

- The requirements include real-time (in the order of seconds, minutes, hours
    vs. daily or weekly) data from multiple systems where the alternative is
    several disjointed integrations or ETL-like implementations

- Any new systems integration effort that would require custom software
    development

If the investment in existing systems or COTS software is large from a time
and/or money perspective, it is worth considering decoupling. Chances are if you
forego decoupling this time around, the challenges with existing system (that is
holding the data, difficult or expensive to change/upgrade, etc.) will only be
greater in the future. Decoupling provides a way to escape technical debt and/or
deepening vendor lock-in and has the advantage of establishing (or joining an
existing) platform architecture that enables incremental change and makes future
changes increasingly affordable.

A message-driven microservices architecture really shines in the face of
real-time data requirements – particularly real-time data requirements involving
multiple systems. It’s worth considering *what the alternative would even look*
like in these cases. Decoupling is the industry best-practice.

Finally, often when you need to integrate systems you are looking at a custom
software development project. In this case, the additional advantages of
domain-defined micros-services and cloud-native “off the shelf infrastructure”
make decoupling a great way to approach this work. Furthermore, the lightweight
architecture and data sharing approach mean what you build now will continue to
pay dividends in the future.

## Conclusion

Digital decoupling is custom software development, but with off-the-shelf
cloud-native infrastructure, architectural principles that focus on embracing
existing systems, and domain-defined integration scope, the economics of build
vs. buy are worth revisiting. In cases of real-time data collaboration or
systems integration, a small investment in decoupling that establishes
microservices and data sharing patterns will enable delivering value frequently
and incrementally. Future needs can be met with greater ease as you capture and
share increasing amounts of domain knowledge.

All good custom software products are a journey where you only start learning
after you start shipping – it’s important to approach decoupling from a mindset
of continuous learning, investment, and value creation (that supports the
investment). Where it makes sense to decouple, sit with your user/stakeholder,
have them paint the future, start small, and begin delivering new value while
embracing your existing system and process landscape. Today’s technical baggage
can return to its role of supporting the organization where it makes sense
without impeding future innovation – you can take back control of your technical
landscape to deliver value quickly and incrementally.
