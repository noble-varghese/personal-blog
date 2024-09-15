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

&nbsp; When I joined **Thena**, we were heavily relying on [Opensearch](https://aws.amazon.com/opensearch-service) and Heroku’s [Mezmo](https://www.mezmo.com/) (formerly LogDNA) to handle all our logging needs. While these tools served us well, there was one major downside: the cost. At over $450 a month, maintaining such an infrastructure wasn't sustainable for a fast-growing company looking to scale smartly. So, I took it upon myself to find a better, more cost-efficient solution that wouldn’t sacrifice performance.

That’s when I discovered **[Quickwit](https://quickwit.io/)**, and I knew this was the game-changer we needed.

## Quickwit: The Game-Changer 🛠️

Quickwit caught my eye because it offered everything we needed but with a much lighter footprint and at a fraction of the cost. Built on top of the **Tantivy** search engine (written in Rust), it’s like Lucene but designed specifically for observability — something we needed in spades. 

Taking charge of the project, I rolled up my sleeves and set out to rebuild our entire logging and observability pipeline around Quickwit. And here’s why it’s been a game-changer for us at Thena:

### 1. Performance + Cost Efficiency = Winning Combo 🏅

The first big win was getting rid of our bloated logging costs. By switching to Quickwit, we decoupled our storage from our compute needs, allowing us to store indexed data on S3-compatible object storage. This gave us two key benefits:
- **Significantly Lower Costs**: Quickwit’s log storage and indexing were far more affordable than our previous solutions.
- **Seamless Scalability**: As our data grew, Quickwit scaled effortlessly in our EKS setup, meaning no more sleepless nights worrying about log volumes.
- **Performance**: Querying through massive datasets at breakneck speed became the norm — something our previous stack struggled with.

I had our new logging system up and running, delivering better performance and saving us a ton of money in the process.

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

### 2. Feature-Packed and Ready for Action 💡

Once I had Quickwit set up, I was blown away by its versatility. Here are just a few of the features that made it the perfect fit for Thena:
- **Grafana Integration**: With Quickwit’s Grafana datasource, I built dynamic, real-time dashboards that let us visualize everything in one place.
- **Log and Trace Ingestion**: Handling both logs and traces was a breeze, giving us a full picture of system performance.
- **Jaeger Integration**: Quickwit fit right into our existing distributed tracing setup with Jaeger, making debugging across services much easier.
- **Elasticsearch-Compatible APIs**: Migrating from OpenSearch was smooth, thanks to Quickwit’s Elasticsearch compatibility.
- **Blazing-Fast Searches**: We needed sub-second search performance for our growing datasets, and Quickwit delivered, letting us search logs directly from object storage without any delays.

### 3. Flexible Indexing for All Our Data 🛠️

Quickwit’s flexibility really shined when I set it up to handle our semi-structured data. With **schemaless indexing** (introduced in version 0.8), I was able to index JSON documents with tons of varying fields, which was crucial for the different types of data Thena handles. This adaptability saved us from having to restructure or compromise on how we log data.

### 4. Migrating the Entire Logging Pipeline: My Journey 🌍

Migrating from our existing setup to Quickwit wasn’t just a switch — it was a full-scale overhaul. Here’s how I tackled it:

- **Proof of Concept**: First, I ran a small-scale test on an EC2 instance, comparing Quickwit’s performance against our existing tools. The results? Quickwit knocked it out of the park.
- **Phased Migration**: I began by moving non-critical log streams to Quickwit, allowing us to test its limits with larger datasets. Quickwit handled everything like a champ.
- **Full Migration**: Once I was confident in Quickwit’s capabilities, I completely transitioned Thena’s logging system over to Quickwit, finally shutting down our Mezmo and OpenSearch setups.

**Challenges?** You bet. Ensuring zero data loss during migration was the biggest hurdle. To overcome this, I ran dual pipelines during the transition, ensuring every single log was captured and fully indexed in Quickwit. No logs left behind!

### 5. Turbocharging Quickwit with Vector 💥

To make our logging pipeline even more robust, I combined Quickwit with **Vector** — a logging powerhouse also written in Rust. Vector became the key to making sure our logs were not only ingested smoothly but also transformed and filtered along the way:

- **Low Footprint**: Vector is way lighter than Fluentbit or Logstash, making it the perfect complement to Quickwit.
- **Log Transformation**: With **Vector Remap Language (VRL)**, I was able to filter and manipulate logs before they were stored, ensuring we only kept what was necessary and secure.
- **Resilience**: Vector offered in-memory log storage when sinks weren’t available, ensuring no logs were ever lost, even in the event of a failure.

## The Final Verdict 🏆

Building this entire observability solution for Thena with Quickwit has been one of the most rewarding challenges I’ve tackled. Not only did I dramatically reduce our costs, but I also significantly boosted our logging performance and flexibility. Quickwit has exceeded every expectation, and the transition from our old system to this new setup was seamless.

For any tech teams out there looking for a powerful, cost-effective observability solution — **Quickwit is the way to go**. It’s changed the game for us at Thena, and I’m proud to have been the one to bring this solution to life.

Thanks for reading, and until next time — keep building and stay curious! 🌟
