> Chapter 1. Introduction


# 1. Introduction

> 介绍

## 1.1. Objective

> 目标

This standard is the specification of the ArchiMate Enterprise Architecture modeling language, a visual language with a set of default iconography-图解 for describing, analyzing, and communicating many concerns-关注点 of Enterprise Architectures as they change over time.

> 该标准是 ArchiMate 企业架构建模语言的规范，这是一种可视化语言，具有一组默认图标，用于描述、分析和交流企业架构随时间变化的许多关注点。

The standard provides a set of entities and relationships with their corresponding iconography for the representation-表示 of Architecture Descriptions.

> 该标准为体系结构描述的表示提供了一组实体和关系及其相应的图示。

The ArchiMate ecosystem also supports an exchange format in XML which allows model and diagram exchange between tools.

> ArchiMate 生态系统还支持 XML 交换格式，允许在工具之间交换模型和图表。



### 1.2. Overview

An Enterprise-企业 Architecture is typically developed because key people have concerns that need to be addressed by the business and IT systems within an organization.

> 企业架构的开发通常是因为关键人员有需要由组织内的业务和IT系统解决的问题。

Such people are commonly **referred to**-把某人叫做 as the “stakeholders” of the Enterprise Architecture.

> 这样的人通常被称为企业架构的“涉众”。

The role of the architect-架构师 is to address these concerns by identifying and refining-细化 the motivation-动机 and strategy expressed by stakeholders, developing an architecture, and creating views of the architecture that show how it addresses and balances stakeholder concerns-关注点.

> 架构师的角色是通过识别和细化涉众表达的动机和策略，开发体系结构，并创建体系结构的视图来处理这些关注点，该视图显示了它如何处理和平衡涉众的关注点。

Without an Enterprise Architecture, it is unlikely that all concerns and requirements are considered and addressed.

> 没有企业架构，就不可能考虑和处理所有的关注点和需求。

---

The ArchiMate Enterprise Architecture modeling language provides a uniform-统一 representation for diagrams that describe Enterprise Architectures.

> ArchiMate 企业架构建模语言为描述企业架构的图表提供了统一的表示。

It includes concepts for specifying-指定 inter-related architectures, specific viewpoints for selected stakeholders, and language customization mechanisms-机制.

> 它包括用于指定相互关联的体系结构的概念、用于选定涉众的特定视点以及语言自定义机制。

It offers an integrated architectural approach that describes and visualizes different architecture domains and their underlying relations and dependencies.

> 它提供了一种集成的体系结构方法，可以描述和可视化不同的体系结构域及其底层关系和依赖性。

Its language framework provides a structuring mechanism for architecture domains, layers-层, and aspects.

> 它的语言框架为体系结构领域、层和方面提供了一种结构化机制。

It distinguishes between the model elements and their notation-符号, to allow for varied, stakeholder-oriented depictions-描述,描绘 of architecture information.

> 它区分了模型元素和它们的符号，允许不同的、面向涉众的体系结构信息描述。

The language uses service-orientation to distinguish and relate the Business, Application, and Technology Layers of Enterprise Architectures, and uses realization relationships to relate concrete-具体的 elements to more abstract elements across these layers.

> 该语言使用面向服务来区分和关联企业架构的业务层、应用程序层和技术层，并使用实现关系将这些层中的具体元素与更抽象的元素关联起来。



### 1.3. Conformance

> 一致性

The ArchiMate language may be implemented in software used for Enterprise Architecture modeling.

> ArchiMate 语言可以在用于企业架构建模的软件中实现。

For the purposes of this standard, the conformance requirements for implementations of the language given in this section apply.

> 为了本标准的目的，本节中给出的语言实现的一致性要求适用。

A conforming implementation:

> 符合标准的实现:

1. Shall support the language structure, generic metamodel, relationships, layers, cross-layer dependencies, and other elements as specified in Chapters [3](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Language-Structure.html), [4](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Generic-Metamodel.html), [5](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Relationships-and-Relationship-Connectors.html), [6](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Motivation-Elements.html), [7](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Strategy-Layer.html), [8](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Business-Layer.html), [9](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Application-Layer.html), [10](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Technology-Layer.html), [11](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Relationships-Between-Core-Layers.html), and [12](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Implementation-and-Migration-Layer.html).
2. Shall support the standard iconography as specified in Chapters [4](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Generic-Metamodel.html), [5](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Relationships-and-Relationship-Connectors.html), [6](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Motivation-Elements.html), [7](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Strategy-Layer.html), [8](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Business-Layer.html), [9](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Application-Layer.html), [10](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Technology-Layer.html), [11](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Relationships-Between-Core-Layers.html), and [12](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Implementation-and-Migration-Layer.html), and summarized in [Appendix A](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Summary-of-Language-Notation.html).
3. Shall support the viewpoint-观点 mechanism-机制 as specified in [Chapter 13](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Stakeholders-Architecture-Views-and-Viewpoints.html).
4. Shall support the language customization mechanisms as specified in [Chapter 14](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Language-Customization-Mechanisms.html) in an implementation-defined manner.
5. Shall support the relationships between elements as specified in [Appendix B](https://pubs.opengroup.org/architecture/archimate3-doc/ch-relationships-Normative.html).
6. May support the example viewpoints described in [Appendix C](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Example-Viewpoints.html) and Chapters [3](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Language-Structure.html), [4](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Generic-Metamodel.html), [5](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Relationships-and-Relationship-Connectors.html), [6](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Motivation-Elements.html), [7](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Strategy-Layer.html), [8](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Business-Layer.html), [9](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Application-Layer.html), [10](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Technology-Layer.html), [11](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Relationships-Between-Core-Layers.html), and [12](https://pubs.opengroup.org/architecture/archimate3-doc/ch-Implementation-and-Migration-Layer.html).

Readers are advised to check The Open Group website for additional conformance and certification requirements referencing this standard.



### 1.4. Normative-规范的,标准的 References-引用,参考

> - 1.4. 引用标准

None.



### 1.5. Terminology

> 术语

For the purposes of this standard, the following terminology definitions apply:

> 为本标准的目的，下列术语定义适用:

|                        |                                                              |
| ---------------------- | ------------------------------------------------------------ |
| Can                    | Describes a possible feature or behavior available to the user.<br>描述用户可用的可能功能或行为。 |
| Deprecated             | Items identified as deprecated-已弃用 may be removed in the next version of this standard.<br>标识为已弃用的项目可能在本标准的下一个版本中被删除。 |
| Implementation-defined | Describes a value or behavior that is not defined by this standard but is selected by an implementor of a software tool.<br>描述未由本标准定义但由软件工具的实现者选择的值或行为。<br>The value or behavior may vary among implementations that conform-遵守,符合 to this standard. <br>值或行为可能在符合此标准的实现中有所不同。<br>A user should not rely on the existence of the value or behavior. <br/>用户不应该依赖于存在的价值或行为。<br/>The implementor shall document such a value or behavior so that it can be used correctly by a user.<br/>实现者应将这样的值或行为记录下来，以便用户能够正确地使用它。 |
| May                    | Describes a feature or behavior that is optional. To avoid ambiguity-歧义, the opposite-相反的 of “may” is expressed as “need not”, instead of “may not”.<br>描述可选的功能或行为。为避免歧义，“may”的反义词用“need not”代替“may not”。 |
| Obsolescent            | Certain features are obsolescent-即将过时的, which means that they may be considered for withdrawal in future versions of this standard. They are retained-保持,保留 because of their widespread-普遍的,广泛的 use, but their use is discouraged.<br>某些特性是过时的，这意味着它们可能会在本标准的未来版本中被考虑撤回。由于它们的广泛使用，它们被保留了下来，但它们的使用是不鼓励的。 |
| Shall                  | Describes a feature or behavior that is a requirement. To avoid ambiguity, do not use “must” as an alternative to “shall”.<br>描述作为需求的特性或行为。为避免歧义，不要用 must 代替 shall。 |
| Shall not              | Describes a feature or behavior that is an absolute prohibition-禁止.<br/>描述绝对禁止的功能或行为。 |
| Should                 | Describes a feature or behavior that is recommended but not required.<br/>描述推荐但非必需的特性或行为。 |
| Will                   | Same meaning as “shall”; “shall” is the preferred term.<br/>与“shall”意思相同;“应该”是首选的术语。 |



### 1.6. Future Directions

> 未来方向

None.

