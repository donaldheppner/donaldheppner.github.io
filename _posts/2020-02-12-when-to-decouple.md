---
layout: post
title:  "When to Decouple Systems"
date:   2020-02-11 10:19:06 -0500
categories: architecture decoupling
---
# What is Digital Decoupling?
- Digital decoupling is creating lightweight domain-defined services, often supported by existing systems, that share information
  - Domain defined (a bounded context within a domain)
  - Embracing existing systems
  - Share (real-time) information
    - Represents a shared concern
- Provides an alternative to directly integrating systems
  - You have a choice
- Allows you to evolve how legacy systems are used without rewriting them; provides a means of overcoming technical debt incrementally
- Achieved leveraging a cloud-native architecture composed of domain defined micro-services and a message-based communication
  - Proven best practices
  - Inherently scalable
  - Low barrier to entry
- Best-supported by “agile” teams: a small, cross-functional team that delivers frequently 
  - Requires iterative/collaborative relationship with your primary stakeholder – they are on the team
  - Does the team belong to IT, or the business it is supporting?
- Provides an alternative to delivering additional business value vs continuing to invest directly in existing commercial off the shelf (COTS) software or legacy systems loaded with technical debt
  - Ex: I can pay for an additional module or functionality or system-specific customization, or I can create a domain-defined service that abstracts the underlying system and allows me to inject my own business-specific (and system agnostic) logic

# Custom Software Development
Digital decoupling _is_ custom software development, with many of its traditional implications:
- Software development is still expensive
- There are up-front costs in establishing core patterns (i.e.: cloud-provisioning, security, etc.)
- Shipping your software is “the end of the beginning” rather than the “beginning of the end” as it is with COTS software deployment
- It requires continuous investment, and should therefore be something you want to invest in continuously because of the ROI
  - You have a backlog or can imagine what one might look like (i.e.: a target state or horizon state)
- Consequently, this approach is best served when the project is tied to generating revenue or unlocking value as opposed to controlling costs
  - Although it can be a cost controlling measure depending on your COTS software fees/alternatives, it is best tied to revenue (and driving revenue) that can support a stable team
  - Existing systems that are doing their job well and integrated as needed can be left alone

## Advantages Over Traditional Software Development
While digital decoupling requires custom software developemtn, it retains some familiar advantages of this appraoch and adds some new ones compared to custom-built products of the past:
- A cloud-native architecture mitigates some of the expense with “off the shelf infrastructure”
- You can start delivering value in weeks-months, rather than the months-years timeframe typical of a large COTS software upgrade, deployment, or migration, or systems integration project
- The approach focuses on embracing and leveraging existing “legacy” systems
- The overall architecture is extremely lightweight; each micro-service can define its own architecture when it comes to integrating with and decoupling dependent systems
- And the software you build still retains its original advantages:
  - Within your control and built-for-purpose
  - Easily customizable

# When To Decouple: How to Choose
- The choice to decouple systems is clearest when the desired business outcome is well defined and any of the following are true:
- The alternative is a 12- to-24-month COTS migration, deployment or upgrade in a competitive area of the business
  - Examples For: Booking for hotels, package tracking for couriers, supply chain for manufacturing
  - Examples Against: E-mail, infrastructure management
- The requirements include access to real-time (in the order of seconds, minutes, hours vs daily or weekly) data from multiple systems where the alternative is several disjointed integrations or ETL-like implementations
  - Furthermore, decoupled systems follow standards for sharing data -- as new requirements surface, they are likely to be met with greater and greater ease
- Any new systems integration effort that would require custom software development
  - The light weight of microservices, scoped down to the business domain/value being sought, leveraging cloud-native architecture is likely to be on par if not cheaper than a custom software development project that exchanges data directly between two systems some other way.
  - Furthermore, not opting for a micro-services, message-based approach foregoes the future benefits of having the exchanged data more broadly available.

# Conclusion
Digital decoupling is custom software development, but with off-the-shelf infrastructure provided by cloud computing and architectural and principles that focus on embracing existing systems and limiting integration scope, the economics of build vs. buy are worth revisiting -- especially when the alternatives are costly COTS software that requires substantial configuration and integration to deploy.