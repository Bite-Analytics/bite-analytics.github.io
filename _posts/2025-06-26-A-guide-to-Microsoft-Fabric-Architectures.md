---
title: "Microsoft Fabric Medallion Architectures"
date: 2025-06-26
categories: [blog]
layout: single
author_profile: true
---


# Choosing the Right Fabric Medallion Architecture: One Workspace or Many?

The medallion architecture—organizing data into **Bronze**, **Silver**, and **Gold** layers—is a foundational design pattern in Microsoft Fabric. It helps teams manage data quality, lineage, and governance by progressively refining data from raw ingestion to curated insights. But how you implement this pattern—especially in terms of workspace and lakehouse design—can significantly impact scalability, security, and operational efficiency.

Let’s explore three common implementation patterns and weigh their trade-offs.

---

## 🧱 Pattern 1: One Workspace, One Lakehouse (All Layers Together)

**Structure**: A single Fabric workspace contains one lakehouse, with folders or schemas representing Bronze, Silver, and Gold layers.

### ✅ Pros:
- **Simplicity**: Easy to manage and deploy, especially for small teams or proof-of-concept projects.
- **Unified View**: All data is accessible in one place, which simplifies development and debugging.
- **Lower Overhead**: Fewer artifacts to manage, reducing administrative burden.

### ❌ Cons:
- **Limited Access Control**: Harder to enforce security boundaries between layers.
- **Scalability Constraints**: As data volume and team size grow, this setup can become unwieldy.
- **Governance Gaps**: Difficult to apply differentiated governance or lifecycle policies per layer.

---

## 🧱 Pattern 2: One Workspace, Three Lakehouses (One per Layer)

**Structure**: A single workspace hosts three separate lakehouses—one each for Bronze, Silver, and Gold.

### ✅ Pros:
- **Layer Isolation**: Clear separation of concerns between ingestion, transformation, and consumption.
- **Improved Governance**: Easier to apply policies and monitor lineage at the lakehouse level.
- **Better Performance Tuning**: Each lakehouse can be optimized for its specific workload.

### ❌ Cons:
- **Moderate Complexity**: Requires more coordination between lakehouses.
- **Shared Workspace Risks**: All layers still share the same workspace-level permissions and capacity.

---

## 🧱 Pattern 3: Separate Workspaces for Each Layer

**Structure**: Each medallion layer resides in its own dedicated workspace, with one lakehouse per workspace.

### ✅ Pros:
- **Maximum Isolation**: Ideal for large organizations with distinct teams managing each layer.
- **Granular Security**: Workspace-level RBAC enables strict access control.
- **Scalable Governance**: Supports enterprise-grade data governance and compliance.

### ❌ Cons:
- **High Complexity**: More moving parts to manage, including cross-workspace data sharing.
- **Increased Overhead**: Requires robust DevOps and orchestration practices.
- **Latency Risk**: Data movement between workspaces may introduce delays.

---

## 🏆 Most Common Pattern

According to Microsoft Learn and internal best practices, the most commonly recommended pattern is:

> **Pattern 2: One Workspace with Three Lakehouses**

This setup strikes a balance between operational simplicity and architectural rigor. It allows for clear separation of data processing stages while maintaining manageable complexity and governance.

---

## 🌍 Real-World Use Cases

- **Pattern 1**: A startup building a quick MVP with a small team and limited governance needs.
- **Pattern 2**: A mid-sized enterprise with a centralized data engineering team and moderate governance requirements.
- **Pattern 3**: A large enterprise with federated data teams, strict compliance, and need for strong isolation.

---

## 📊 Decision Matrix

| Criteria                  | Pattern 1: One Lakehouse | Pattern 2: Three Lakehouses | Pattern 3: Three Workspaces |
|---------------------------|--------------------------|-----------------------------|-----------------------------|
| Simplicity                | ✅ High                  | ⚖️ Medium                   | ❌ Low                      |
| Governance                | ❌ Low                   | ✅ Medium                   | ✅ High                     |
| Scalability               | ❌ Limited               | ✅ Good                     | ✅ Excellent                |
| Security Isolation        | ❌ Minimal               | ⚖️ Moderate                 | ✅ Strong                   |
| Ideal For                 | POCs, small teams        | Most orgs                   | Large, regulated orgs       |

---

## 🧠 Expert Tips

- Use naming conventions like `bronze_`, `silver_`, `gold_` for tables to maintain clarity.
- Consider using shortcuts or views in Gold to abstract complexity from consumers.
- Use Fabric pipelines or Dataflows Gen2 to orchestrate transitions between layers.
- Leverage Fabric’s lineage view to track data flow across lakehouses.

---

## ⚙️ Performance & Cost Considerations

- **Pattern 1** may lead to performance bottlenecks as all workloads share the same lakehouse.
- **Pattern 2** allows tuning each lakehouse for its specific workload (e.g., ingestion vs. analytics).
- **Pattern 3** introduces overhead but enables cost attribution and scaling per layer.

---

## 🔗 Integration with Other Fabric Features

- **Power BI**: Gold layer is typically the source for semantic models.
- **Data Activator**: Can monitor Silver or Gold layers for real-time triggers.
- **KQL DBs**: Useful for telemetry or log data in the Bronze layer.
- **Notebooks & Pipelines**: Ideal for orchestrating transformations across layers.

---

## 📣 Call to Action

Have you implemented a medallion architecture in Fabric? Share your experience by opening a pull request or starting a discussion!

Want to contribute diagrams or templates? Fork this repo and help the community grow!

---

*Let’s build better data products—one layer at a time.*


And remember: the best architecture is the one that aligns with your business goals while enabling agility and trust in your data.

---


