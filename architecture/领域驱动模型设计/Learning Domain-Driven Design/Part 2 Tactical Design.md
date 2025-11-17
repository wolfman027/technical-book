# Part 2 Tactical Design

> 部分 2 战术设计

In Part I, we discussed the “what” and “why” of software: you learned to analyze business domains, identify subdomains and their strategic value, and turn the knowledge of business domains into the design of bounded contexts—software components implementing different models of the business domain.

> 在第一部分中，我们讨论了软件的“什么”和“为什么”:您学会了分析业务领域、识别子领域及其战略价值，并将业务领域的知识转化为限界上下文的设计——实现业务领域不同模型的软件组件。

In this part of the book, we will turn from strategy to tactics: the “how” of software design:

> 在本书的这一部分，我们将从战略转向战术：“如何”进行软件设计:

- In Chapters 5 through 7, you will learn business logic implementation patterns that allow the code to speak the ubiquitous language of its bounded context.

  > 在第5章到第7章中，您将学习业务逻辑实现模式，这些模式允许代码使用其有界上下文中的通用语言。

  Chapter 5 introduces two patterns that accommodate-适应 a relatively-相当地,相对地 simple business logic: transaction script and active record. 

  > 第5章介绍了两种适应相对简单业务逻辑的模式：事务脚本和活动记录。

  Chapter 6 moves to more challenging cases and presents the domain model pattern: DDD’s way of implementing complex business logic.

  > 第6章转向更具挑战性的案例，并介绍了领域模型模式：DDD 实现复杂业务逻辑的方式。

  In Chapter 7, you will learn to expand the domain model pattern by modeling the dimension of time.

  > 在第7章中，您将学习通过对时间维度进行建模来扩展域模型模式。

- In Chapter 8, we will explore the different ways to organize a bounded context’s architecture: the layered architecture, ports & adapters, and CQRS patterns.

  > 在第8章中，我们将探讨组织有界上下文架构的不同方法：分层架构、端口和适配器以及CQRS模式。

  You will learn the essence of each architectural pattern and in which cases each pattern should be used.

  > 您将了解每种体系结构模式的本质，以及在哪些情况下应该使用每种模式。

- Chapter 9 will discuss technical concerns and implementation strategies for orchestrating-精心策划 the interactions among components of a system.

  > 第9章将讨论协调系统组件之间交互的技术问题和实现策略。

  You will learn patterns supporting the implementation of bounded context integration patterns, how to implement reliable publishing of messages, and patterns for defining complex, cross-component workflows.

  > 您将学习支持实现限界上下文集成模式的模式、如何实现可靠的消息发布，以及用于定义复杂的跨组件工作流的模式。



