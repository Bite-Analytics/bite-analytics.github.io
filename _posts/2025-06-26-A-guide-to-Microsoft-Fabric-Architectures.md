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

## 🧠 Final Thoughts

Choosing the right medallion architecture pattern in Fabric isn’t just a technical decision—it’s a strategic one. Consider your team structure, data governance needs, and long-term scalability when selecting a pattern.

And remember: the best architecture is the one that aligns with your business goals while enabling agility and trust in your data.

---

*Want to contribute or share your experience with Fabric medallion patterns? Open a pull request or start a discussion in the Issues tab!*

