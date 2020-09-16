---
title: "The simplest solution is usually the best"
date: 2020-09-14T20:53:21-04:00
draft: false
description : "The simplest solution is usually the best"
tags : [
    "Architecture",
    "System Design",
    "Application Design"
]
author: "Borko"
authorLink: "https://www.b3o.ca"
featuredImage: "featured-image"
featuredImagePreview: "featured-image"
resources:
- name: "featured-image"
  src: "featured-image.jpg"
- name: "featured-image"
  src: "featured-image.jpg"

lightgallery: true

toc:
  auto: false
---

{{< admonition type=quote title="Quote" open=true >}}
*The greatest ideas are the simplest.*
― William Golding, Lord of the Flies
{{< /admonition >}}

## Design for today's requirements

Any product or application solution should be designed and built to meet *today's* business requirements. Do not try to predict the future.

Product owners/solution architects/developers sometimes have a habit to over-design the architecture and implement "useful" features. I've been guilty of this on a number of occasions. However, these features do not add any value *today*. With the pace of business changes in today's world, priorities may shift at any time. Thus the anticipated future value of these features *may never be realized*. These extra features only increase development and testing effort and time, and risk reducing quality of the code. Worse, they can also increase operational and maintenance costs.

As architects and engineers, we shouldn't complicate our work without clear and specific need.  However, on the flip side, if our experience or gut feeling convinces us that something is missing and should be part of the solution, then the issue should be raised and addressed. Part of our job is to draw attention to any ambiguities and concerns so that the requirements can be revisited for confirmation with business/customer/end-user stakeholders. A too-common example of this are non-functional requirements around things like instrumentation/observability or backup and data retention. These aspects are often initially overlooked until they are crucially needed later.

## Anticipate future change

Designing for today's requirements is critical.  However, we need to acknowledge and be cognizant of the fact that things are *going to change in future*. 

This means that we need to apply "best-practices" when designing and building our solutions (and save ourselves pains and headaches in the future). In order to facilitate future evolution of our software and systems, we need to ensure that it is designed in a decoupled and extensible way. We should ask ourselves: "Am I going to understand this twelve months from now?"

Consequently, if we implement an extensible solution, then when the inevitable changes come, incorporating the new requirements into our system will not be as a complex and gargantuan task as it could have been.

{{< admonition type=quote title="Quote" open=true >}}
*Everything should be made as simple as possible, but not simpler.*
― Albert Einstein
{{< /admonition >}}

## Too simple is as bad as too complex

Implementing the simplest solution is not the same as implementing the solution as quickly as possible. Oversimplification or implementing a solution haphazardly can result in a something that doesn't fully realize the business or end-user requirements. To bring long-term value, we have to be mindful of concerns like maintainability, scalability, operability, performance, cost optimization, etc. and ensure we incorporate those requirements into our solutions as appropriate.