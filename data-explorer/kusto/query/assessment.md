---
Title:  Writing Assessment by Chava Nebenzahl
Description:  This article has been revised to enhance clarity and readability. 
MS Reviewer: 
MS Topic: Reference
Date: 16/01/2025
---
# Kusto Query Language (KQL)

This article provides an overview of KQL and offers practical exercises to help you begin writing queries. 
- To access the query environment, go to the [Azure Data Explorer Web UI](https://dataexplorer.azure.com/).
- For instructions on using KQL, see [Tutorial: Learn common operators](tutorials/learn-common-operators.md).

KQL is a powerful tool for exploring and querying various data types, discovering patterns, identifying anomalies, and creating statistical models. It is intuitive and user-friendly, ideal for querying telemetry, metrics, and logs. KQL excels in text search, time-series operations, analytics, aggregation, geospatial analysis, and vector similarity searches. Its schema structure, similar to SQL, uses databases, tables, and columns as foundational components, making it an optimal choice for data analysis.

## Creating Kusto Query Statements

The most common query statement is a tabular expression, which consists of tabular datasets and zero or more operators. Each operator processes tabular input and produces tabular output. Operators are chained using a `|` (pipe), with data flowing through each operator, being filtered or manipulated at each stage.

A Kusto query is a read-only request that processes data and returns results, written in plain text. It follows a simple, automatable data-flow model. Query statements can be compared to a funnel, where data is refined step-by-step through each operator. The order of operators is critical, and the final output is a refined result.

In KQL, [query statements](statements.md) are classified into three types: 

1. A [tabular expression statement](tabular-expression-statements.md)
1. A [let statement](let-statement.md)
1. A [set statement](set-statement.md)

All query statements are separated by a `;` (semicolon), and only impact the query being executed.

Here is an example of a query:

> [!div class="nextstepaction"]
> <a href="https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAAwsuyS/KdS1LzSspVuCqUSjPSC1KVQguSSwqCcnMTVVISi0pT03NU9BISSxJLQGKaBgZGJjrGhrqGhhqKujpKaCJG4HENZENKklVsLVVUHLz8Q/ydHFUUgDZkpxfmlcCAIItD6l6AAAA" target="_blank">Run the query</a>

```kusto
StormEvents 
| where StartTime between (datetime(2007-11-01) .. datetime(2007-12-01))
| where State == "florida"  
| count 
```

|Count|
|-----|
|   28|

**NOTE**: KQL is case-sensitive for all elements, including table names, column names, operators, functions, and other components.

This query consists of a single tabular expression statement: 
- The statement begins by referencing a table called *StormEvents* and includes several operators, such as [`where`](where-operator.md) and [`count`](count-operator.md), each separated by a pipe.
- The data rows for the source table are first filtered based on the value in the *StartTime* column and then by the value in the *State* column.
- In the last line, the query returns a table with a single column and a single row, which contain the count of the remaining rows.

For information about application query statements, see [Application query statements](statements.md#application-query-statements).

## Management Commands

Management commands have a distinct syntax separate from the KQL, identified by beginning with a dot (`.`), which cannot be used to start a query. This prevents security vulnerabilities by ensuring management commands cannot be embedded within queries.

Not all management commands modify data or metadata. Many, like `.show` commands, display metadata or data. For example, `.show tables` lists all tables in the current database. Unlike Kusto queries, [management commands](management/index.md)  request Kusto to process or modify data and metadata. 

The following management command creates a new Kusto table with two columns, `Level` and `Number`:

```kusto
.create table Logs (Level:string, Text:string)
```

For more information on management commands, see [Management commands overview](../management/index.md).

## Using KQL in Different Services

KQL is utilized by various other Microsoft services. For specific information on the use of KQL in these environments, refer to the following links:

[Log queries in Azure Monitor](/azure/azure-monitor/logs/log-query-overview)
[Kusto Query Language in Microsoft Sentinel](/azure/sentinel/kusto-overview)
[Understanding the Azure Resource Graph query language](/azure/governance/resource-graph/concepts/query-language)
[Proactively hunt for threats with advanced hunting in Microsoft 365 Defender](/microsoft-365/security/defender/advanced-hunting-overview)
[CMPivot queries](/mem/configmgr/core/servers/manage/cmpivot-overview#queries)

## Related Documentation

* [Tutorial: Learn common operators](tutorials/learn-common-operators.md)
* [Tutorial: Use aggregation functions](tutorials/use-aggregation-functions.md)
* [KQL quick reference](kql-quick-reference.md)
* [SQL to Kusto Query Language cheat sheet](sql-cheat-sheet.md)
* [Query best practices](best-practices.md)
