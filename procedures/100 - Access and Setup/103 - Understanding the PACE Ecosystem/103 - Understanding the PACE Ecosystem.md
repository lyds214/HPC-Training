---
title: "103 - Understanding the PACE Ecosystem"
---

# Understanding the PACE Ecosystem
PACE stands for Partnership for an Advanced Computing Environment. It is Georgia Tech's research computing organization, and it provides three things:

- **Compute and storage -** Access to CPU and GPU resources, along with personal and shared project storage designed to handle the I/O demands of research workloads.
- **A support team -** The Research Computing Facilitation team provides consultations, workshops, and email support to help researchers get the most out of available resources.
- **A software stack -** Python, R, Julia, Jupyter, Anaconda, and a wide range of licensed and open-source software are already installed and configured, so you can spend less time compiling and more time working on your research.

---

## Three clusters, three purposes
![Cluster Flow]({{ '/assets/img/clusterFlow.png' | relative_url }})

PACE operates several distinct computing clusters. While they use the same core technologies, each cluster is designed for a different purpose and has its own eligibility and access requirements.

| Cluster | Purpose | Cost | Who can apply | Hardware highlights |
|---|---|---|---|---|
| **Phoenix** | General-purpose research cluster | Credit system with a free tier; no-cost backfill partition | GT-affiliated research projects | Intel and AMD CPU nodes, NVIDIA H200/H100/A100/V100/L40S GPUs, NVMe/SAS storage |
| **Firebird** | Research involving controlled unclassified information (CUI), export-controlled (ITAR) software, or other sensitive data | Credit system; no-cost backfill partition for paying users | GT-affiliated research projects | CPU nodes similar to Phoenix, NVIDIA H200/A100/RTX6000 GPUs, independent per-project storage |
| **ICE** | Instructional Cluster Environment, for coursework, workshops, and the AI Makerspace | No cost | Any GT-affiliated faculty member, or a makerspace project | CPUs and GPUs, Infiniband, NVMe |

> **A fourth cluster, Hive, was decommissioned in September 2025 and no longer appears in current PACE documentation.**

This training track is built around ICE. It is the cluster that course instructors request on behalf of their classes. It costs nothing to use, and it is where you will run the exercises in the rest of this guide. What you learn here carries over directly to Phoenix or Firebird if you later work with a research group that uses one of those instead, since all three clusters run the same Slurm-based scheduling underneath.

---

## Who requests access, and how

- **Phoenix -** A PI or faculty sponsor fills out the [PACE Account Creation Request Form](https://pace.gatech.edu/ice-cluster/) on behalf of their students, researchers, or staff. Individual students do not self-request.
- **Firebird -** Access is arranged directly with PACE by emailing `pace-support@oit.gatech.edu` since CUI and ITAR projects carry extra requirements.
- **ICE -** The course instructor applies to use ICE for their class. Students should not fill out the ICE application themselves. Instructors outside the College of Computing use the standard ICE application; instructors teaching within the College of Computing go through the TSO's instructional team instead.

---

## How the cluster is organized

Once you are logged in, you are actually touching two different kinds of machines, and mixing them up is one of the more common early mistakes.

- **Head node.** This is the machine you land on when you SSH in or log into OnDemand (for example, `login-phoenix-rh9.pace.gatech.edu` on Phoenix; ICE has its own login node). It is a shared resource used by everyone logged in at that moment. Use it for light tasks like editing files, organizing data, or checking on jobs. Do not run computations, installs, compiles, or visualizations here. You would be competing with everyone else on that same shared machine, and that kind of work belongs on a compute node anyway.
- **Compute nodes.** These are the machines that actually run your work. When you submit a job, Slurm allocates you your own CPUs, GPUs, and RAM on a compute node. Your data is visible from both the head node and every compute node, so nothing needs to be copied manually for a job to find its files.

---

## Slurm: the reason there is a queue at all

Unlike your laptop, a cluster is shared by dozens, sometimes hundreds, of people at once. Slurm is the workload manager that arbitrates that sharing fairly. You tell it what you need (CPUs, memory, wall time, GPUs if any), and it holds your job until that exact set of resources is free, then runs it for exactly as long as you asked.

That is the whole idea in one sentence, and it is why submitting a job feels different from just running a script locally. The mechanics of actually writing and submitting a Slurm job start in [**200 - Running Your First Job**]({{ '/procedures/200 - Running Your First Job/' | relative_url }}); this page exists so the vocabulary (head node, compute node, scheduler, queue) is already familiar by the time you get there.


> **PACE note:** This page is based on the PACE Orientation deck dated Spring 2026 (March 2026 update). Cluster availability, hardware, and access processes change over time, so confirm anything access- or hardware-specific against the [PACE website](https://pace.gatech.edu) or current KB documentation before relying on it for something time-sensitive.
