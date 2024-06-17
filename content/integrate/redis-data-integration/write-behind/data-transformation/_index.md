---
Title: Data transformation
aliases: null
alwaysopen: false
categories:
- docs
- integrate
- rs
- rdi
description: null
group: di
hideListLinks: false
linkTitle: Data transformation
summary: Redis Data Integration keeps Redis in sync with the primary database in near
  real time.
type: integration
weight: 30
---

The key functionality that RDI performs is mapping the data coming from [Debezium Server](https://debezium.io/documentation/reference/stable/operations/debezium-server.html) (representing a Source Database row data or row state change) into a Redis key with a value of [Hash]({{< relref "/develop/data-types/hashes" >}}) or [JSON]({{< relref "/develop/data-types/json/" >}}).
There are two types of data transformations in RDI:

1. By default, each source row is converted into one [Hash]({{< relref "/develop/data-types/hashes" >}}) or one JSON key in Redis.
  This conversion uses the Debezium schema-based conversion. The incoming data includes the schema and RDI uses a set of handlers to automatically convert each source column to a Redis Hash field or JSON type based on the Debezium type in the schema. See
  [data type conversion]({{< relref "/integrate/redis-data-integration/write-behind/reference/data-types-conversion" >}})
  for a full reference on these conversions.

1. If the user wants to add or modify this default mapping, RDI provides declarative data transformations. These transformations are represented in YAML files. Each file contains a job, which is a set of transformations per source table. See
[declarative transformations]({{< relref "/integrate/redis-data-integration/write-behind/data-transformation/data-transformation-pipeline" >}}) for more information.

{{< image filename="/images/rdi/data-transformation-flow.png" >}}

## More info

