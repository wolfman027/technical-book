# Part 1 Strategic Design

> 部分 1 战略设计

*There* *is no sense in talking about the solution before we agree on the problem, and no sense talking about the implementation steps before we agree on the solution.*

—Efrat Goldratt-Ashlag1

> 在我们就问题达成一致之前谈论解决方案是没有意义的，在我们就解决方案达成一致之前谈论实施步骤也是没有意义的



The domain-driven design (DDD) methodology can be divided into two main parts: strategic design and tactical design.

> 领域驱动设计(DDD)方法可以分为两个主要部分：战略设计和战术设计。

The strategic aspect of DDD deals with answering the questions of “what?” and “why?”—what software we are building and why we are building it.

The tactical part is all about the “how”—how each component is implemented.



We will begin our journey by exploring domain-driven design patterns and principles of strategic design:

> 我们将从探索领域驱动的设计模式和战略设计原则开始我们的旅程：

In Chapter 1, you will learn to analyze a company’s business strategy: what value it provides to its consumers and how it competes with other companies in the industry.

> 在第一章中，你将学习分析一家公司的商业战略：它为消费者提供了什么价值，以及它如何与同行业中的其他公司竞争。

We will identify finer-grained-细粒度 business building blocks, evaluate their strategic value, and analyze how they affect different software design decisions.

> 我们将识别细粒度的业务构建块，评估它们的战略价值，并分析它们如何影响不同的软件设计决策。

---

Chapter 2 introduces domain-driven design’s essential practice for gaining an understanding of the business domain: the *ubiquitous-普遍存在的 language*.

> 第2章介绍了领域驱动设计的基本实践，以获得对业务领域的理解：通用语言。

You will learn how to cultivate-培养,建立 a ubiquitous language and use it to foster-促进,培养 a shared understanding among all project-related stakeholders.

> 您将学习如何培养一种通用语言，并使用它来促进所有项目相关利益相关者之间的共同理解。

---

Chapter 3 discusses another domain-driven design core tool: the *bounded context* pattern.

> 第三章讨论了另一个领域驱动设计的核心工具：“有界上下文”模式。

You will learn why this tool is essential for cultivating-培养,建立 a ubiquitous language and how to use it to transform discovered knowledge into a model of the business domain.

> 您将了解为什么这个工具对于培养通用语言至关重要，以及如何使用它将发现的知识转换为业务领域的模型。

Ultimately, we will leverage bounded contexts to design coarse-grained-粗略的,大概的,粗粒度 components of the software system.

> 最后，我们将利用有界上下文来设计软件系统的粗粒度组件。

---

In Chapter 4, you will learn technical and social constraints that affect how system components can be integrated, and integration patterns that address different situations and limitations.

> 在第 4 章中，您将学习影响系统组件如何集成的技术和社会约束，以及处理不同情况和限制的集成模式。

We will discuss how each pattern influences collaboration among software development teams and the design of the components’ APIs.

> 我们将讨论每种模式如何影响软件开发团队之间的协作以及组件 API 的设计。

The chapter closes by introducing the *context map*: a graphical notation that plots communication between the system’s bounded contexts and provides a bird’s-eye view of the project’s integration and collaboration landscapes.

> 本章最后介绍了“上下文图”：这是一种图形化的符号，描绘了系统的边界上下文之间的通信，并提供了项目集成和协作景观的鸟瞰图。

---

