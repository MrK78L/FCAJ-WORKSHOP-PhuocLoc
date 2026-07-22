---
title: "Event 1"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Reflection Report: “FCAJ Community Day – Conference Call”

## Event Purpose

The event provided a space for FCAJ members, mentors, and technology professionals to share practical knowledge about artificial intelligence, AWS services, cloud architecture, security, and real-world product development. It also created opportunities for participants to exchange ideas and learn from completed projects and industry experience.

## Speakers and Topics

- **Mr. Tịnh** – *Build a Second Brain*
- **Hải Anh** – *Friendly AI Assistant with Amazon QuickSight*
- **Thịnh** – *From Edge to Origin: CloudFront as Your Foundation*
- **VIB Team** – *36 Hours with LotusHacks – Building UTMorpho from Idea to Reality*
- **Đào Đức** – *Deep-Dive Talk: How Does an LLM Actually Work?*
- **Cát Vy** – *Enterprise-Grade Multi-Agent System*

## Key Highlights

### AI application mindset

Using a large language model effectively requires clear, specialized context instead of a large amount of unrelated information. Developers should avoid blindly copying source code or plugins from the Internet without understanding their purpose and architecture.

### The probabilistic nature of LLMs

Large language models are inherently non-deterministic. Even when `temperature` is set to zero, responses may still differ because of GPU processing and optimization mechanisms used by API providers.

### Enterprise multi-agent architecture

A single agent may not handle every complex task effectively. Enterprise systems can divide responsibilities among specialized agents for analysis, research, orchestration, and risk management. Clear boundaries and coordination are necessary for reliable performance.

### AWS infrastructure and security

Amazon CloudFront does more than accelerate content delivery. It can also help protect the origin, reduce direct exposure, absorb distributed traffic, and integrate with other AWS security controls. Architecture and cost should be reviewed before selecting pricing and protection options.

### Practical AI development through a hackathon

The VIB Team demonstrated an application that used AI to generate and modify HTML/CSS interfaces. Important lessons included controlling token consumption, limiting features to the core product value, and preventing AI-generated code from becoming unnecessarily complex.

## What I Learned

### Context is essential

AI performs best when it receives specific context, a clear role, constraints, and a precise objective.

### AI output must be verified

AI-generated data and code should be reviewed by both the system and its users. Applications should include validation, fallback behavior, and exception handling to manage invalid or unexpected output.

### Security must be included from the beginning

Real-world AI systems must address data leakage, prompt injection, access control, and audit trails. Security should be part of the architecture rather than an addition made after development.

### A production product is different from a demo

A complete application needs a clear architecture, well-defined responsibilities, appropriate security, and a focus on core value. Adding too many technologies or features can make the system difficult to maintain.

## Application to My Work

### Improving backend development

When building complex backend systems, including applications that integrate AI, controllers and business logic should handle failures safely. AI-generated formats such as JSON must be validated carefully to prevent invalid responses from causing system errors.

### Designing and implementing UI/UX

AI can assist with drafting and refining interfaces in Figma or HTML/CSS, but it needs explicit design rules and constraints. This helps produce cleaner, more consistent output and limits unnecessary code generation.

### Managing cloud infrastructure

CloudFront can be considered for distributing static content and images while reducing direct origin exposure. Security, monitoring, scalability, and cost should be considered from the earliest architecture-design stage.

## Event Experience

Participating in the event was a new and valuable experience. It provided practical perspectives on AI, AWS services, and designing projects for real environments.

### Learning from experienced speakers

The speakers shared knowledge in an engaging and approachable way. Their sessions covered AI, CloudFront, secure system design, and lessons learned from real project development.

### Practical technical experience

The VIB Team's project was particularly impressive. Within 36 hours, the team created an application with an attractive drag-and-drop interface, a multi-agent workflow, and a broad set of working features.

### Main lesson

Production development is very different from preparing a demonstration. In addition to writing code, a team must consider security, clear architecture, operational reliability, and the core value being delivered. Features and technologies should be selected purposefully instead of being added without a clear need.

### Event Photos

*Add event photos here.*

> Overall, the event provided useful technical knowledge and helped me improve the way I think about system design, security, and real-world product development.
