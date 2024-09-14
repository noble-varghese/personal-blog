---
author: Noble Varghese
pubDatetime: 2024-09-14T15:22:00Z
modDatetime: 2024-09-14T15:22:00Z
title: How Quickwit Transformed Our Observability Game and Saved Us Big Bucks
slug: quickwit-transformed-our-obs
featured: false
draft: false
tags:
  - quickwit
  - opensource
  - observability
description: Saving costs by moving to opensource alternatives of elasticsearch.
---


Hey there, fellow tech enthusiasts! 🚀

As a team of innovators, we're building something new and exciting, but we also have to be smart about our expenses. In our early days, keeping costs under control while maintaining high performance was a balancing act. That's where observability comes into play - it's crucial for us to keep tabs on how everything's running smoothly.

Initially, we were leaning heavily on [Opensearch](https://aws.amazon.com/opensearch-service) (thanks to AWS) and Heroku's [Mezmo](https://www.mezmo.com/) (formerly LogDNA) for our logging needs. While these tools served us well with solid log storage, speedy searches, and powerful aggregations, the costs quickly added up - over $450 a month, to be precise. For a growing startup, that was a significant expense. So, we started hunting for an open-source alternative that could deliver the same high performance without the high price tag. That's when [Quickwit](https://quickwit.io/) caught our eye.

## Enter Quickwit: The Game-Changer

Quickwit is a breath of fresh air in the observability landscape. Built on top of [Tantivy](https://github.com/quickwit-oss/tantivy)- an open-source search engine library written in Rust - Quickwit is akin to Lucene but designed for observability with a minimal footprint. Here's why Quickwit has quickly become our go-to tool:

### 1. Performance Meets Cost-Efficiency

Quickwit shines with its low overhead and high-speed performance. Unlike traditional solutions, it stores indexed data on S3-compatible object storage. This decoupling of storage and compute not only enhances performance but also reduces costs.
Quickwit offered several key advantages that made it the ideal solution for us:

- **Lower Cost Storage**: Quickwit's optimized log storage and indexing allowed us to store more data without breaking the bank.
- **Scalability**: Quickwit's architecture enabled seamless horizontal scaling in EKS, effortlessly handling our growing log volumes.
- **Performance**: Even with massive datasets, Quickwit let us query logs at lightning speed, supercharging our ability to diagnose and squash issues.

<style>
  .bigger-image {
    width: 100%; /* Adjust width as needed */
    max-width: 100%;
    display: block;
    margin: 0 auto; /* Centers the image */
  }
</style>

<div>
  <img src="/assets/performance-metrics-quickwit.png" class="bigger-image" alt="Quickwit prometheus metrics">
</div>

### 2. Feature-Rich Out of the Box

Quickwit doesn't skimp on features. It offers:

- **Datasource for Grafana**: Integrates seamlessly, allowing for dynamic and customizable dashboards.
- **Log and Trace Ingestion**: Handles both logs and traces efficiently.
- **Jaeger Integration**: Works well with Jaeger, another fantastic open-source tool for distributed tracing.
- **Elasticsearch-Compatible APIs**: Ensures smooth compatibility with Elasticsearch queries.
- **Sub-Second Searches**: Provides lightning-fast search capabilities directly from object storage.

### 3. Flexibility in Indexing

One of Quickwit's (from 0.8) standout features is its ability to handle semi-structured data. With schemaless indexing, you can index JSON documents with an arbitrary number of fields without compromising performance. This flexibility is crucial for dealing with the diverse data formats we encounter.

### 4. The Transition Process

We implemented a phased migration approach:

- **Proof of Concept**: We deployed Quickwit alongside our existing setup on an EC2 instance to validate its performance and integration.
- **Partial Migration**: We gradually shifted less critical log streams to Quickwit to test its capacity for handling larger data volumes. Quickwit can also be load-tested with tracegen.
- **Full Migration**: After successful testing, we completely transitioned all logs to Quickwit and decommissioned our Mezmo and OpenSearch setups.

**Challenges During Migration**: Ensuring zero data loss during the transition was our top priority. We temporarily ran dual pipelines to guarantee all logs were captured and conducted comparison tests to verify we weren't missing any data.

### 5. Enhancing Quickwit with Vector

We didn't stop there. To supercharge our logging pipeline and to ensure resilience, we combined Quickwit with Vector from Datadog. Vector is another gem written in Rust and brings some incredible advantages to the table:

- Low Footprint: Vector is lightweight compared to other solutions like Fluentbit and Logstash, thanks to its Rust-based design.
  Vector Remap Language (VRL): This powerful feature allows us to transform, filter, and manipulate logs before indexing, making our data processing much more efficient and also enabled us to mask any sensitive data that might have been added to the logs.
- Versatile Sources: Vector offers extensive options for log sources, enhancing our data ingestion capabilities.
  Disaster Recovery: Vector can temporarily store logs in-memory if one or more sinks (destination log storage) are unavailable, ensuring full data security in the event of a disaster.

## The Verdict

Quickwit has been a game-changer for our observability needs. It's been performing beyond our expectations and has proven to be a cost-effective alternative to our previous solutions. As we continue to grow, having a reliable and efficient logging setup like Quickwit ensures we stay on top of our game without burning a hole in our budget.
That's all for now, folks! If you're a startup or a tech team looking for an observability tool that's both powerful and cost-effective, give Quickwit a look. It might just be the solution you've been searching for.
Catch you next time! 🌟
