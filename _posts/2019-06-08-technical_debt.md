---
layout: post_1
title: 07 - Technical Debt
date: 2019-06-08 -0400
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/7---Technical-Debt-e49g1d/a-agqips
description: "We explore the topic of software quality and discover what technical debt actually means."
---

## What is Technical Debt?
Wikipedia: “concept that reflects the implied cost of additional rework caused by choosing and easy solution now instead of using a better approach that would take longer.”

Metaphor to financial debt, in which you amass interest on your resources and engineering costs if debt is not repaid by refactoring, making yourself a risky lender and making it harder to pay back your debt later on.

Conceptually, if we want to build something on top of a shaky foundation, it takes longer to implement a new feature properly. TLDR: Do something quick and dirty to unlock something specific in the short-term, but we know it will bite us in the long-term.

## Software Quality
- External quality: perceived by user, performance, stability, managed by product people.
- Internal quality: perceived by technical people. Extending or maintaining the code easier/harder. Tests, architectural style, code complexity.

Refactoring only addresses internal quality and doesn’t add any external quality, so it can be hard to justify to someone non-technical, since they don’t see the benefits.

Eventually internal quality leaks out to affect external quality, in that it takes longer to develop features, performance or security may suffer, there may be limitations to what can be built due to how costly it would be to go back and fix past decisions.

Commercial success is tied to external quality, whereas technical debt is tied to internal quality, __at first__. They are independant in that it’s mostly about number of resources to deliver the final result. But since resources cost money, it’s a ultimately a business decision.

## Is Tech Debt Bad?
Going into debt isn’t always bad. When you put a mortgage on a house, you amass a large debt, but it’s usually a benefit in that it’s an investment, you don’t pay rent, etc. If you take out a loan to blow it off at the casino, you’re in trouble.

It can be a strategy if you are aware of it. It may be more important to get to market as soon as possible and sacrifice code quality and maintainability, and if the risk is paid off, we can pay the debt off later.

The interest rate is only uncovered when you change legacy code. IF you don’t change the code, no one sees or has to know. The person to pay back the debt isn’t necessarily the one who created it. This sparked the devops movement, which effectively recognized this form of technical debt and attempted to increase awareness of it.

So it’s not always a bad thing.

## Martin fowler’s 4 Technical debt quadrants
- Deliberate & Reckless ( "We don't have time for design")
- Deliberate & Prudent ("We must ship now and deal with consequences (later)")
- Inadvertent & Reckless ("What's Layering?")
- Deliberate & Prudent ("Now we know how we should have done it")

## Why does tech debt happen?
- Don’t understand domain or requirements
- Business/time pressure
- Not familiar with patterns or technology
- Badly-designed software architecture, tightly coupled,
- Software decay

# Approaches of dealing with technical debt?
- Rewrite vs incremental improvement.
- Tests are the bare minimum
- Never let bus factor happen
- Keep things DRY
- Having uncoupled systems
- Traditional software engineering advice
- Communicate effectively as a technical person in your organization
- It’ll always be there, so deal with it so you can sleep at night.
