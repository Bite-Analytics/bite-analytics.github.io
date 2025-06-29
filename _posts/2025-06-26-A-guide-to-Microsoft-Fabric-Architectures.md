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

![Pattern 1](pattern_1.png)

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

![Pattern 2](pattern_2.png)

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

![Pattern 3](pattern_3.png)

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

## 🔍 Real-World Use Cases

- **Pattern 1**: Small startup building a quick MVP.
- **Pattern 2**: Mid-sized enterprise with centralized data engineering.
- **Pattern 3**: Large enterprise with federated data teams and strict compliance needs.

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

---

## 📈 Performance & Cost Considerations

- **Data refresh latency**: Lower in Pattern 1, more controllable in Patterns 2 and 3.
- **Compute cost**: Easier to isolate and optimize in Patterns 2 and 3.
- **Storage optimization**: Better with separate lakehouses or workspaces.

---

## 🧩 Integration with Other Fabric Features

- **Power BI**: Semantic models can be layered on Gold lakehouse.
- **Data Activator**: Can trigger alerts from Silver or Gold layers.
- **Real-time analytics**: KQL DBs can be integrated at the Bronze or Silver stage.

---

## 🗣️ Call to Action

Want to contribute or share your experience with Fabric medallion patterns?  
Open a pull request or start a discussion in the Issues tab!



