> Chapter 16. Data Mesh
>
> 数据网格

So far in this book, we have discussed models used to build operational systems.

> 到目前为止，在本书中，我们已经讨论了用于构建操作系统的模型。

Operational systems implement real-time transactions that manipulate the system’s data and orchestrate its day-to-day interactions with its environment.

> 操作系统实现实时事务，操作系统的数据并编排其与环境的日常交互。

These models are the **online transactional processing (OLTP)** data.

> 这些模型是联机事务处理(OLTP)数据。

Another type of data that deserves-值得,应受 attention and proper-适当的 modeling is online analytical processing (OLAP) data.

> 另一种值得关注和适当建模的数据类型是在线分析处理(OLAP)数据。

---

In this chapter, you will learn about the analytical data management architecture called data mesh.

> 在本章中，您将学习称为数据网格的分析数据管理架构。

You will see how the data mesh–based architecture works and how it differs from the more traditional OLAP data management approaches.

> 您将看到基于数据网格的体系结构是如何工作的，以及它与更传统的 OLAP 数据管理方法的不同之处。

Ultimately-最终,最后, you will see how domain-driven design and data mesh accommodate-顺应,适应 each other.

> 最后，您将看到领域驱动的设计和数据网格是如何相互适应的。

But first, let’s see what these analytical data models are and why we can’t just reuse the operational models for analytical use cases.

> 但首先，让我们看看这些分析数据模型是什么，以及为什么我们不能仅仅为分析用例重用操作模型。



# Analytical Data Model Versus Transactional Data Model

> 分析数据模型与事务数据模型

They say knowledge is power.

他们说知识就是力量。

Analytical data is the knowledge that gives companies the power to leverage accumulated-积累,积攒 data to gain insights into how to optimize the business, better understand customers’ needs, and even make automated decisions by training machine learning (ML) models.

> 分析数据是一种知识，它使公司能够利用积累的数据来深入了解如何优化业务，更好地了解客户需求，甚至通过训练机器学习(ML)模型做出自动化决策。

---

The analytical models (OLAP) and operational models (OLTP) serve different types of consumers, enable the implementation of different kinds of use cases, and are therefore designed following other design principles.

> 分析模型(OLAP)和操作模型(OLTP)服务于不同类型的消费者，支持实现不同类型的用例，因此按照其他设计原则进行设计。

---

Operational models are built around the various entities from the system’s business domain, implementing their lifecycles and orchestrating their interactions with one another.

> 操作模型是围绕来自系统业务领域的各种实体构建的，实现它们的生命周期并编排它们彼此之间的交互。

These models, depicted in Figure 16-1, are serving operational systems and hence have to be optimized to support real-time business transactions.

> 如图16-1所示，这些模型为操作系统提供服务，因此必须进行优化以支持实时业务事务。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723415268451.jpg)

*Figure 16-1. A relational database schema describing the relationships between entities in an operational model*

Analytical models are designed to provide different insights into the operational systems.

> 分析模型旨在提供对操作系统的不同见解。

Instead of implementing real-time transactions, an analytical model aims to provide insights into the performance of business activities and, more importantly, how the business can optimize its operations to achieve greater value.

> 分析模型的目的不是实现实时事务，而是提供对业务活动性能的洞察，更重要的是，提供业务如何优化其操作以实现更大的价值。

---

From a data structure perspective, OLAP models ignore the individual business entities and instead focus on business activities by modeling fact tables and dimension tables.

> 从数据结构的角度来看，OLAP模型忽略了单个业务实体，而是通过建模事实表和维度表来关注业务活动。

We’ll take a closer look at each of these tables next.

> 接下来，我们将仔细研究这些表。



## Fact Table

> 事实表

Facts represent business activities that have already happened.

> 事实代表已经发生的商业活动。

Facts are similar to the notion of domain events in the sense that both describe things that happened in the past.

> 事实与领域事件的概念相似，因为它们都描述了过去发生的事情。

However, contrary to domain events, there is no stylistic requirement to name facts as verbs in the past tense-时态.

> 然而，与领域事件相反，在语体上没有要求将事实命名为过去时的动词。

Still, facts represent activities of business processes.

> 事实仍然表示业务流程的活动。

For example, a fact table Fact_CustomerOnboardings would contain a record for each new onboarded-参与其中 customer and Fact_Sales a record for each committed sale.

> 例如，事实表 Fact_CustomerOnboardings 将包含每个新加入客户的记录，而 Fact_Sales 将包含每个已承诺销售的记录。

Figure 16-2 shows an example of a fact table.

> 图 16-2 展示了一个事实表的示例。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723415898063.jpg)

*Figure 16-2. A fact table containing records for cases solved by a company’s support desk*

Also, similar to domain events, fact records are never deleted or modified: analytical data is append-only data: the only way to express that current data is outdated is to append a new record with the current state.

> 此外，与领域事件类似，事实记录永远不会被删除或修改：分析数据是仅追加的数据：表示当前数据过时的唯一方法是追加具有当前状态的新记录。

Consider the fact table Fact_CaseStatus in Figure 16-3.

> 考虑图16-3中的事实表 Fact_CaseStatus。

It contains the measurements of the statuses of support requests through time.

> 它包含随时间变化的支持请求状态的度量。

There is no explicit verb in the fact name, but the business process captured by the fact is the process of **taking care of**-处理 support cases.

> 事实名称中没有明确的动词，但事实捕获的业务流程是处理支持案例的流程。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723416155562.jpg)

*Figure 16-3. A fact table describing state changes during the lifecycle of a support case*

Another significant difference between the OLAP and OLTP models is the granularity-粒度 of the data.

> OLAP和OLTP模型之间的另一个重要区别是数据的粒度。

Operational systems require the most precise data to handle business transactions.

> 操作系统需要最精确的数据来处理业务事务。

For analytical models, aggregated data is more efficient in many use cases.

> 对于分析模型，聚合数据在许多用例中更有效。

For example, in the Fact_CaseStatus table shown in Figure 16-3, you can see that the snapshots are taken every 30 minutes.

> 例如，在图16-3 所示的 Fact_CaseStatus 表中，您可以看到快照每30分钟拍摄一次。

The data analysts working with the model decide what level of granularity will best suit their needs.

> 使用模型的数据分析人员决定哪种粒度级别最适合他们的需求。

Creating a fact record for each change of the measurement—for example, each change of a case’s data— would be wasteful in some cases and even technically impossible in others.

> 为度量的每次更改(例如，每次更改案例的数据)创建事实记录在某些情况下是浪费的，在其他情况下甚至在技术上是不可能的。



## Dimension Table

> 维度表

Another essential building block of an analytical model is a dimension.

> 分析模型的另一个基本构建块是维度。

If a fact represents a business process or action (a verb), a dimension describes the fact (an adjective-形容词).

> 如果事实表示业务流程或操作(动词)，则维度描述事实(形容词)。

---

The dimensions are designed to describe the facts’ attributes and are referenced as a foreign key from a fact table to a dimension table.

> 维度被设计用来描述事实的属性，并且作为外键从事实表引用到维度表。

The attributes modeled as dimensions are any measurements or data that is repeated across different fact records and cannot fit in a single column.

> 建模为维度的属性是在不同事实记录中重复出现的任何测量值或数据，并且不能放在单个列中。

For example, the schema in Figure 16-4 augments-增加,增大 the SolvedCases fact with its dimensions.

> 例如，图16-4中的模式增加了 SolvedCases 事实的维度。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723502385048.jpg)

*Figure 16-4.* *The* *SolvedCases fact surrounded by its dimensions*

The reason for the high normalization of the dimensions is the analytical system’s need to support flexible querying.

> 维度高度规范化的原因是分析系统需要支持灵活的查询。

That’s another difference between operational and analytical models.

> 这是操作模型和分析模型的另一个区别。

It’s possible to predict-预言,预计 how an operational model will be queried to support the business requirements.

> 可以预测如何查询操作模型以支持业务需求。

The querying patterns of the analytical models are not predictable.

> 分析模型的查询模式是不可预测的。

The data analysts need flexible ways of looking at the data, and it’s hard to predict what queries will be executed in the future.

> 数据分析人员需要灵活地查看数据，而且很难预测将来将执行哪些查询。

As a result, the normalization supports dynamic querying and filtering, and grouping the facts data across the different dimensions.

> 因此，规范化支持动态查询和过滤，以及跨不同维度对事实数据进行分组。



## Analytical Models

> 分析模型

The table structure depicted in Figure 16-5 is called the *star schema*.

> 图16-5中描述的表结构称为**星型模式**。

It is based on the many-to-one relationships between the facts and their dimensions: each dimension record is used by many facts; a fact’s foreign key points to a single dimension record.

> 它基于事实与其维度之间的多对一关系:每个维度记录由许多事实使用；事实的外键指向单维记录。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723502746096.jpg)

*Figure 16-5.* *The* *many-to-one relationship between facts and their dimensions*

Another predominant-明显的,主要的 analytical model is the snowflake schema.

> 另一个主要的分析模型是雪花模式。

The snowflake schema is based on the same building blocks: facts and dimensions.

> 雪花模式基于相同的构建块：事实和维度。

However, in the snowflake schema, the dimensions are multilevel: each dimension is further-进一步 normalized into more fine-grained dimensions, as shown in Figure 16-6.

> 然而，在雪花模式中，维度是多层的：每个维度被进一步规范化为更细粒度的维度，如图16-6所示。

---

As a result of the additional normalization, the snowflake schema will use less space to store the dimension data and is easier to maintain.

> 由于进行了额外的规范化，雪花模式将使用更少的空间来存储维度数据，并且更易于维护。

However, querying the facts’ data will require joining more tables, and therefore, more computational resources are needed.

> 然而，查询事实数据将需要连接更多的表，因此需要更多的计算资源。

---

Both the star and snowflake schemas allow data analysts to analyze business performance, gaining insights into what can be optimized and built into business intelligence (BI) reports.

> 星型和雪花型模式都允许数据分析人员分析业务性能，从而深入了解哪些内容可以被优化并内置于商业智能(BI)报告中。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723503367360.jpg)

*Figure 16-6. Multilevel dimensions in the* *snowflake* *schema*



# Analytical Data Management Platforms

> 分析数据管理平台

Let’s shift the discussion from analytical modeling to data management architectures that support generating and serving analytical data.

> 让我们将讨论从分析建模转移到支持生成和服务分析数据的数据管理架构。

In this section, we will discuss two common analytical data architectures: data warehouse-仓库 and data lake.

> 在本节中，我们将讨论两种常见的分析数据架构：数据仓库和数据湖。

You will learn the basic working principles of each architecture, how they differ from each other, and the challenges of each approach.

> 您将了解每种体系结构的基本工作原理、它们之间的不同之处，以及每种方法的挑战。

Knowledge of how the two architectures work will build the foundation for discussing the main topic of this chapter: the data mesh paradigm-典范,范例 and its interplay with domain-driven design.

> 了解这两种架构是如何工作的，将为讨论本章的主要主题奠定基础：数据网格范式及其与领域驱动设计的相互作用。



## Data Warehouse

> 数据仓库

The data warehouse (DWH) architecture is relatively straightforward-简单的,易懂的.

> 数据仓库(DWH)体系结构相对简单。

Extract data from all of the enterprise’s operational systems, transform the source data into an analytical model, and load the resultant data into a data analysis–oriented database.

> 从所有企业的操作系统中提取数据，将源数据转换为分析模型，并将结果数据加载到面向数据分析的数据库中。

This database is the data warehouse.

> 这个数据库就是数据仓库。

---

This data management architecture is based primarily on the extract-提取,提炼-transform-load (ETL) scripts.

> 这个数据管理体系结构主要基于提取-转换-加载(ETL)脚本。

The data can come from various sources: operational databases, streaming events, logs, and so on.

> 数据可以来自各种来源：操作数据库、流事件、日志等等。

In addition to translating the source data into a facts/dimensions-based model, the transformation step may include additional operations such as removing sensitive data, deduplicating records, reordering events, aggregating fine-grained events, and more. 

> 除了将源数据转换为基于事实/维度的模型之外，转换步骤还可能包括其他操作，例如删除敏感数据、重复数据删除、重新排序事件、聚合细粒度事件等等。

In some cases, the transformation may require temporary storage for the incoming data.

> 在某些情况下，转换可能需要临时存储传入的数据。

This is known as the staging area.

> 这就是所谓的集结区。

---

The resultant data warehouse, shown in Figure 16-7, contains analytical data covering-涵盖 all of the enterprise’s business processes. 

> 生成的数据仓库，如图16-7所示，包含涵盖所有企业业务流程的分析数据。

The data is exposed using the SQL language (or one of its dialects-方言,土话) and is used by data analysts and BI engineers.

> 数据使用 SQL 语言(或其方言之一)公开，供数据分析师和BI工程师使用。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723674120212.jpg)

*Figure 16-7. A typical enterprise data warehouse architecture*

The careful reader will notice that the data warehouse architecture shares some of the challenges discussed in Chapters 2 and 3.

> 细心的读者会注意到，数据仓库架构与第2章和第3章中讨论的一些挑战相同。

---

First, at the heart of the data warehouse architecture is the goal of building an enterprise-wide model.

> 首先，数据仓库体系结构的核心目标是构建企业范围的模型。

The model should describe the data produced by all of the enterprise’s systems and address all of the different use cases for analytical data.

> 该模型应该描述由所有企业系统产生的数据，并处理分析数据的所有不同用例。

The analytical model enables, for example, optimizing the business, reducing operational costs, making intelligent business decisions, reporting, and even training ML models.

> 例如，分析模型支持优化业务、降低运营成本、做出明智的业务决策、报告，甚至训练ML模型。

As you learned in Chapter 3, such an approach is impractical-不明智的,不切实际的 for anything by the smallest organizations.

> 正如您在第3章中所了解的，这种方法对于任何小型组织来说都是不切实际的。

Designing a model for the task at hand, such as building reports or training ML models, is a much more effective and scalable approach.

> 为手头的任务设计模型，例如构建报告或训练ML模型，是一种更有效和可扩展的方法。

---

The challenge of building an all-encompassing-包含,包括 model can be partly addressed by the use of data marts-集市.

> 构建一个包罗万象的模型的挑战可以通过使用数据集市部分解决。

A data mart is a database that holds data relevant for well-defined analytical needs, such as analysis of a single business department.

> 数据集市是一种数据库，其中包含与定义良好的分析需求相关的数据，例如对单个业务部门的分析。

In the data mart model shown in Figure 16-8, one mart is populated-充满,填充 directly by an ETL process from an operational system, while another mart extracts-提取,提炼 its data from the data warehouse.

> 在图16-8所示的数据集市模型中，一个集市由来自操作系统的ETL进程直接填充，而另一个集市则从数据仓库中提取其数据。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723674601634.jpg)

*Figure 16-8.* *The* *enterprise data warehouse architecture augmented-增加,扩大 with data marts*

When the data is ingested-摄取,吸收 into a data mart from the enterprise data warehouse, the enterprise-wide model still needs to be defined in the data warehouse.

> 当数据从企业数据仓库被摄取到数据集市时，仍然需要在数据仓库中定义企业范围的模型。

Alternatively, data marts can implement dedicated ETL processes to ingest-摄取,吸收 data directly from the operational systems.

> 或者，数据集市可以实现专用的ETL流程来直接从操作系统中摄取数据。

In this case, the resultant model makes it challenging to query data across different marts—for example, across different departments—as it requires a cross-database query and significantly-显著地,意味深长地 impacts performance.

> 在这种情况下，生成的模型使跨不同市场(例如跨不同部门)查询数据变得困难，因为它需要跨数据库查询，并且会显著影响性能。

---

Another challenging aspect of the data warehouse architecture is that the ETL processes create a strong coupling between the analytical (OLAP) and the operational (OLTP) systems.

> 数据仓库体系结构的另一个具有挑战性的方面是，ETL流程在分析(OLAP)和操作(OLTP)系统之间创建了强耦合。

The data consumed by the ETL scripts is not necessarily exposed through the system’s public interfaces.

> ETL脚本使用的数据不一定通过系统的公共接口公开。

Often, DWH systems simply fetch all the data residing-居住,居留 in the operational systems’ databases.

> 通常，DWH系统只是获取驻留在操作系统数据库中的所有数据。

The schema used in the operational database is not a public interface, but rather an internal implementation detail.

> 操作数据库中使用的模式不是公共接口，而是内部实现细节。

As a result, a slight change in the schema is destined-指定,预定 to break the data warehouse’s ETL scripts.

> 因此，模式中的微小变化注定会破坏数据仓库的ETL脚本。

Since the operational and analytical systems are implemented and maintained by somewhat distant organizational units, the communication between the two is challenging and leads to lots of friction-分歧,摩擦 between the teams.

> 由于操作系统和分析系统是由距离较远的组织单位实现和维护的，因此两者之间的通信具有挑战性，并导致团队之间的许多摩擦。

This communication pattern is shown in Figure 16-9.

> 这种通信模式如图16-9所示。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1723675220199.jpg)

*Figure 16-9. Data warehouse populated by fetching data directly from operational databases, ignoring the integration-oriented public interfaces*

The data lake architecture addresses some of the shortcomings-缺点,短处 of the data warehouse architecture.

> 数据湖体系结构解决了数据仓库体系结构的一些缺点。



## Data Lake

> 数据湖

As a data warehouse, the data lake architecture is based on the same notion of ingesting-摄取,吸收 the operational systems’ data and transforming it into an analytical model.

> 作为数据仓库，数据湖体系结构基于摄取操作系统数据并将其转换为分析模型的相同概念。

However, there is a conceptual difference between the two approaches.

> 然而，这两种方法之间存在概念上的差异。

---

A data lake–based system ingests the operational systems’ data.

> 基于数据湖的系统摄取操作系统的数据。

However, instead of being transformed **right away**-立刻,马上 into an analytical model, the data is persisted in its raw-原始的 form, that is, in the original operational model.

> 但是，数据不会立即转换为分析模型，而是以原始形式(即原始操作模型)保存。

---

Eventually, the raw data cannot fit the needs of data analysts.

> 最终，原始数据无法满足数据分析师的需求。

As a result, it is the job of the data engineers and the BI engineers to **make sense of**-理解,弄懂 the data in the lake and implement the ETL scripts that will generate analytical models and feed-提供 them into a data warehouse.

> 因此，数据工程师和BI工程师的工作是理解湖中的数据，并实现生成分析模型并将其提供给数据仓库的ETL脚本。

Figure 16-10 depicts a data lake architecture.

> 数据湖架构如图16-10所示。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1724019575848.jpg)

*Figure 16-10. Data lake architecture*

Since the operational systems’ data is persisted in its original, raw form and is transformed only afterward-以后,后来, the data lake allows working with multiple, task-oriented analytical models.

> 由于操作系统的数据以其原始的原始形式保存，并且只在之后进行转换，因此数据湖允许使用多个面向任务的分析模型。

One model can be used for reporting, another for training ML models, and so on.

> 一个模型可用于报告，另一个用于训练 ML 模型，等等。

Furthermore, new models can be added in the future and initialized with the existing raw data.

> 此外，未来还可以添加新的模型，并使用现有的原始数据进行初始化。

---

That said, the delayed generation of analytical models increases the complexity of the overall system.

> 也就是说，分析模型的延迟生成增加了整个系统的复杂性。

It’s not uncommon for data engineers to implement and support multiple versions of the same ETL script to accommodate-适应,容纳 different versions of the operational model, as shown in Figure 16-11.

> 对于数据工程师来说，实现和支持同一个ETL脚本的多个版本以适应不同版本的操作模型是很常见的，如图16-11所示。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1724019896661.jpg)

*Figure 16-11. Multiple versions of the same ETL script accommodating* *different* *versions of the operational model*

Furthermore, since data lakes are schema-less—there is no schema imposed-强制推行,强制实行 on the incoming data—and there is no control over the quality of the incoming data, the data lake’s data becomes chaotic at certain levels of scale.

> 此外，由于数据湖没有模式(没有模式强加给传入数据)，并且无法控制传入数据的质量，因此数据湖的数据在某些规模级别上变得混乱。

Data lakes make it easy to ingest data but much more challenging to make use of it.

> 数据湖使获取数据变得容易，但要使用数据却更具挑战性。

Or, as is often said, a data lake becomes a data swamp-沼泽,湿地.

> 或者，正如人们常说的那样，数据湖变成了数据沼泽。

The data scientist’s job becomes orders of magnitude-规模 more complex-复杂的 to **make sense of**-理解,弄懂 the chaos and to extract useful analytical data.

> 数据科学家的工作变得更加复杂，要理解混乱并提取有用的分析数据。



## Challenges of Data Warehouse and Data Lake Architectures

> 数据仓库和数据湖架构的挑战

Both data warehouse and data lake architectures are based on the assumption that the more data that is ingested for analytics, the more insight the organization will gain.

> 数据仓库和数据湖体系结构都是基于这样的假设：用于分析的数据越多，组织获得的洞察力就越多。

Both approaches, however, tend to break under the weight of “big” data.

> 然而，这两种方法都倾向于在“大”数据的重压下崩溃。

The transformation of operational to analytical models converges-汇聚,集中 to thousands of unmaintainable, ad hoc ETL scripts at scale.

> 从操作模型到分析模型的转换在规模上汇聚了数千个不可维护的、特别的ETL脚本。

---

From a modeling perspective, both architectures trespass-侵入,干涉 the boundaries of the operational systems and create dependencies on their implementation details.

> 从建模的角度来看，这两种体系结构都跨越了操作系统的边界，并在它们的实现细节上创建依赖关系。

The resultant coupling to the implementation models creates friction between the operational and analytical systems teams, often to the point of preventing changes to the operational models for the sake of not breaking the analysis system’s ETL jobs.

> 与实现模型的耦合在操作系统和分析系统团队之间产生了摩擦，通常为了不破坏分析系统的ETL作业而阻止对操作模型的更改。

---

To make matters worse-更糟糕, since the data analysts and data engineers belong to a separate organizational unit, they often lack the deep knowledge of the business domain possessed-拥有,持有 by the operational systems’ development teams.

> 更糟糕的是，由于数据分析师和数据工程师属于不同的组织单位，他们通常缺乏操作系统开发团队所拥有的业务领域的深入知识。

Instead of the knowledge of the business domain, they are specialized-专门研究 mainly in big data tooling.

> 他们没有业务领域的知识，而是主要专注于大数据工具。

---

Last but not least, the coupling to the implementation models is especially acute-尖锐的,严重的,敏锐的 in domain-driven design–based projects, in which the emphasis is on continuously evolving and improving the business domain’s models.

> 最后但并非最不重要的一点是，在领域驱动的基于设计的项目中，与实现模型的耦合特别尖锐，在这些项目中，重点是不断发展和改进业务领域的模型。

As a result, a change in the operational model can have unforeseen consequences in the analytical model.

> 因此，操作模型中的更改可能会对分析模型产生不可预见的后果。

Such changes are frequent in DDD projects and often result in friction between R&D and data teams.

> 这种变化在DDD项目中很常见，并且经常导致研发团队和数据团队之间的摩擦。

---

These limitations of data warehouses and data lakes inspired-激发,使产生 a new analytical data management architecture: data mesh.

> 数据仓库和数据湖的这些限制激发了一种新的分析数据管理架构：数据网格。



# Data Mesh

> 数据网格

The data mesh architecture is, in a sense, domain-driven design for analytical data.

> 从某种意义上说，数据网格体系结构是分析数据的领域驱动设计。

As the different patterns of DDD draw boundaries and protect their contents, the data mesh architecture defines and protects model and ownership boundaries for analytical data.

> 当DDD的不同模式绘制边界并保护其内容时，数据网格体系结构定义并保护分析数据的模型和所有权边界。

---

The data mesh architecture is based on four core principles: decompose-分解 data around domains, data as a product-产品, enable autonomy-自治, and build an ecosystem-生态系统.

> 数据网格架构基于四个核心原则：围绕域分解数据、数据作为产品、实现自治和构建生态系统。

Let’s discuss each principle in detail.

> 让我们详细讨论每个原则。



## Decompose Data Around Domains

> 围绕域分解数据

Both the data warehouse and data lake approaches aim to unify-联合 all of the enterprise’s data into one big model.

> 数据仓库和数据湖方法都旨在将企业的所有数据统一到一个大模型中。

The resultant analytical model is ineffective for all the same reasons as an enterprise-wide operational model is.

> 由于与企业范围的操作模型相同的原因，结果分析模型是无效的。

Furthermore, gathering data from all systems into one location blurs-模糊 the ownership boundaries of the various data elements.

> 此外，将来自所有系统的数据收集到一个位置模糊了各种数据元素的所有权边界。

---

Instead of building a monolithic analytical model, the data mesh architecture calls for leveraging the same solution we discussed in Chapter 3 for operational data: use multiple analytical models and align them with the origin of the data.

> 数据网格架构不需要构建一个单一的分析模型，而是需要利用我们在第3章中讨论的用于操作数据的相同解决方案：使用多个分析模型，并使它们与数据的来源保持一致。

This naturally aligns the ownership boundaries of the analytical models with the bounded contexts’ boundaries, as shown in Figure 16-12.

> 这自然地使分析模型的所有权边界与有界上下文的边界保持一致，如图16-12所示。

When the analysis model is decomposed according to the system’s bounded contexts, the generation of the analysis data becomes the responsibility of the corresponding product teams.

> 当分析模型根据系统的有界上下文进行分解时，分析数据的生成就变成了相应产品团队的责任。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1724021883543.jpg)

*Figure 16-12. Aligning the ownership boundaries of the analytical models with the bounded contexts’ boundaries*

Each bounded context now owns its operational (OLTP) and analytical (OLAP) models.

> 每个有界上下文现在都拥有自己的操作(OLTP)和分析(OLAP)模型。

Consequently, the same team owns the operational model, now in charge of transforming it into the analytical model.

> 因此，同样的团队拥有操作模型，现在负责将其转换为分析模型。



## Data as a Product

> 数据即产品

The classic data management architectures make it difficult to discover, understand, and fetch quality analytical data.

> 传统的数据管理架构使得发现、理解和获取高质量的分析数据变得困难。

This is especially acute in the case of data lakes.

> 这在数据湖的情况下尤其严重。

---

The data as a product principle calls for treating the analytical data as a first-class citizen-公民.

> 数据作为产品的原则要求把分析数据当作一等公民来对待。

Instead of the analytical systems having to get the operational data from dubious-可疑的,靠不住的 sources (internal database, logfiles, etc.), in a data mesh–based system the bounded contexts serve the analytical data through well-defined output ports, as shown in Figure 16-13.

> 分析系统不必从可疑的来源(内部数据库，日志文件等)获取操作数据，在基于数据网格的系统中，有界上下文通过定义良好的输出端口为分析数据提供服务，如图16-13所示。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1724193020161.jpg)

*Figure 16-13. Polyglot data endpoints exposing the analytical data to the consumers*

Analytical data should be treated the same as any public API：

> 分析数据应与任何公共API一样对待:

- It should be easy to discover the necessary endpoints: the data output ports.

  > 应该很容易发现必要的端点：数据输出端口。

- The analytical endpoints should have a well-defined schema describing the served data and its format.

  > 分析端点应该有一个定义良好的模式来描述所服务的数据及其格式。

- The analytical data should be trustworthy, and as with any API, it should have defined and monitored service-level agreements (SLAs).

  > 分析数据应该是可信的，并且与任何API一样，它应该定义和监视服务水平协议(SLAs)。

- The analytical model should be versioned as a regular-通常的 API and correspondingly manage integration-breaking changes in the model.

  > 分析模型应该作为常规API进行版本化，并相应地管理模型中破坏集成的更改。

Furthermore, since the analytical data is treated as a product, it has to address the needs of its consumers.

> 此外，由于分析数据被视为产品，因此它必须满足其消费者的需求。

The bounded context’s team is in charge of ensuring that the resultant model addresses the needs of its consumers.

> 有界上下文的团队负责确保生成的模型满足其消费者的需求。

Contrary to the data warehouse and data lake architectures, with data mesh, accountability for data quality is a top-level concern.

> 与数据仓库和数据湖体系结构相反，对于数据网格，数据质量的责任是最重要的问题。

---

The goal of the distributed data management architecture is to allow the fine-grained analytical models to be combined to address the organization’s data analysis needs.

> 分布式数据管理体系结构的目标是允许将细粒度分析模型组合起来，以满足组织的数据分析需求。

For example, if a BI report should reflect data from multiple bounded contexts, it should be able to easily fetch their analytical data if needed, apply local transformations, and produce the report.

> 例如，如果 BI 报告应该反映来自多个有界上下文的数据，那么如果需要，它应该能够轻松地获取分析数据，应用本地转换，并生成报告。

---

Finally, different consumers may require the analytical data in different forms.

> 最后，不同的消费者可能需要不同形式的分析数据。

Some may prefer to execute SQL queries, others to fetch analytical data from an object storage service, and so on.

> 有些人可能更喜欢执行SQL查询，有些人更喜欢从对象存储服务中获取分析数据，等等。

As a result, the data products have to be polyglot-多种语言的, serving the data in formats that suit different consumers’ needs.

> 因此，数据产品必须是多语言的，以适合不同消费者需求的格式提供数据。

---

To implement the data as a product principle, product teams require adding data-oriented-朝向,面对 specialists.

> 为了将数据作为产品原则实现，产品团队需要添加面向数据的专家。

That’s the missing piece in the cross-functional teams puzzle-拼图, which traditionally includes only specialists related to the operational systems.

> 这是跨职能团队拼图中缺失的一块，传统上只包括与运营系统相关的专家。



## Enable Autonomy

> 使自治

The product teams should be able to both create their own data products and consume data products served by other bounded contexts.

> 产品团队既应该能够创建自己的数据产品，也应该能够使用由其他有界上下文提供服务的数据产品。

Just as in the case of bounded contexts, the data products should be interoperable-互操作的.

> 正如在有界上下文的情况下一样，数据产品应该是可互操作的。

---

It would be wasteful, inefficient, and hard to integrate if each team builds their own solution for serving analytical data.

> 如果每个团队都为分析数据构建自己的解决方案，这将是浪费的、低效的，并且很难集成。

To prevent this from happening, a platform is needed to abstract the complexity of building, executing, and maintaining interoperable data products.

> 为了防止这种情况发生，需要一个平台来抽象构建、执行和维护可互操作数据产品的复杂性。

Designing and building such a platform is a considerable-相当大的,相当重要的 undertaking and requires a dedicated-专门的 data infrastructure platform team.

> 设计和构建这样一个平台是一项相当大的工作，需要一个专门的数据基础设施平台团队。

---

The data infrastructure platform team should be in charge of defining the data product blueprints, unified-统一 access patterns, access control, and polyglot storage that can be leveraged by product teams, as well as monitoring the platform and ensuring that the SLAs and objectives are met.

> 数据基础设施平台团队应该负责定义数据产品蓝图、统一访问模式、访问控制和产品团队可以利用的多语言存储，以及监控平台并确保满足 SLAs 和目标。



## Build an Ecosystem

> 构建生态系统

The final step to creating a data mesh system is to appoint a federated-联合的 governance body to enable interoperability-互用性 and ecosystem thinking-思维 in the domain of the analytical data.

> 创建数据网格系统的最后一步是指定一个联合治理机构，以启用分析数据领域中的互操作性和生态系统思维。

Typically, that would be a group consisting of the bounded contexts’ data and product owners and representatives of the data infrastructure platform team, as shown in Figure 16-14.

> 通常，这将是一个由有界上下文的数据和产品所有者以及数据基础设施平台团队的代表组成的组，如图16-14所示。

---

The governance group is in charge of defining the rules to ensure a healthy and interoperable ecosystem.

> 治理组负责定义规则，以确保健康和可互操作的生态系统。

The rules have to be applied to all data products and their interfaces, and it’s the group’s responsibility to ensure adherence-遵守,坚持 to the rules throughout the enterprise.

> 这些规则必须应用于所有数据产品及其接口，并且团队有责任确保在整个企业中遵守这些规则。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1724194337095.jpg)

> *Figure 16-14.* *The* *governance group, which ensures that the distributed data analytics ecosystem is interoperable, healthy, and serves the organization’s needs*



## Combining Data Mesh and Domain-Driven Design

> 结合数据网格和领域驱动设计

These are the four principles that the data mesh architecture is based on.

> 这是数据网格体系结构所基于的四个原则。

The emphasis on defining boundaries, and encapsulating the implementation details behind well-defined output ports, makes it evident-清楚的,显然的 that the data mesh architecture is based on the same reasoning as domain-driven design.

> 强调定义边界和封装定义良好的输出端口背后的实现细节，这显然表明数据网格体系结构基于与领域驱动设计相同的推理。

Furthermore, some of the domain-driven design patterns can greatly support implementing the data mesh architecture.

> 此外，一些领域驱动的设计模式可以极大地支持数据网格体系结构的实现。

---

First and foremost-首先,首要的, the ubiquitous language and the resultant domain knowledge are essential for designing analytical models. 

> 首先，通用语言和由此产生的领域知识对于设计分析模型至关重要。

As we discussed in the data warehouse and data lake sections, domain knowledge is lacking in traditional architectures.

> 正如我们在数据仓库和数据湖部分所讨论的，传统体系结构缺乏领域知识。

---

Second, exposing a bounded context’s data in a model that is different from its operational model is the open-host pattern.

> 其次，在与其操作模型不同的模型中公开有界上下文的数据是开放主机模式。

In this case, the analytical model is an additional-附加的 published language.

> 在这种情况下，分析模型是一种附加的已发布语言。

---

The CQRS pattern makes it easy to generate multiple models of the same data.

> CQRS 模式可以很容易地生成相同数据的多个模型。

It can be leveraged to transform the operational model into an analytical model.

> 可以利用它将操作模型转换为分析模型。

The CQRS pattern’s ability to generate models **from scratch**-从零开始 makes it easy to generate and serve multiple versions of the analytical model simultaneously, as shown in Figure 16-15.

> CQRS 模式从零开始生成模型的能力使得同时生成和提供多个版本的分析模型变得容易，如图16-15所示。

![](/Users/h.a.hu/Library/CloudStorage/OneDrive-Accenture (2024-8-21 17:45)/Documents/accenture-new/Knowledge-Ocean/构建系统软技能/DDD/Learning Domain-Driven Design/img/1724203185615.jpg)

*Figure 16-15. Leveraging the CQRS pattern to simultaneously serve the analytical data in two* *different* *schema versions*

Finally, since the data mesh architecture combines the different bounded contexts’ models to implement analytical use cases, the bounded context integration patterns for operational models apply for analytical models as well.

> 最后，由于数据网格体系结构结合了不同的有界上下文模型来实现分析用例，因此操作模型的有界上下文集成模式也适用于分析模型。

Two product teams can evolve their analytical models in partnership-合伙（关系）.

> 两个产品团队可以合作发展他们的分析模型。

Another can implement an anticorruption layer to protect itself from an ineffective analytical model.

> 另一个可以实现一个反腐败层来保护自己不受无效分析模型的影响。

Or, on the other hand, the teams can go their separate ways and produce duplicate implementations of analytical models.

> 或者，另一方面，团队可以采用各自的方式，生成分析模型的重复实现。



# Conclusion

> 总结

In this chapter, you learned the different aspects of designing software systems, in particular, defining and managing analytical data.

> 在本章中，您学习了设计软件系统的不同方面，特别是定义和管理分析数据。

We discussed the predominant-主要的,明显的 models for analytical data, including the star and snowflake schemas, and how the data is traditionally managed in data warehouses and data lakes.

> 我们讨论了分析数据的主要模型，包括星型和雪花型模式，以及传统上如何在数据仓库和数据湖中管理数据。

---

The data mesh architecture aims to address the challenges of the traditional data management architectures.

> 数据网格体系结构旨在解决传统数据管理体系结构的挑战。

At its core, it applies the same principles as domain-driven design but to analytical data: decomposing the analytical model into manageable units and ensuring that the analytical data can be reliably accessed and used through its public interfaces. 

> 在其核心，它应用与领域驱动设计相同的原则，但适用于分析数据：将分析模型分解为可管理的单元，并确保可以通过其公共接口可靠地访问和使用分析数据。

Ultimately, the CQRS and bounded context integration patterns can support implementing the data mesh architecture.

> 最终，CQRS 和有界上下文集成模式可以支持实现数据网格体系结构。

