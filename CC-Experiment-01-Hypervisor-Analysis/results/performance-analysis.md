# Performance Analysis

## 1. Overview

This document presents the CPU performance results obtained from the two virtualization environments used in the experiment:

- **Type-1 Hypervisor:** Proxmox VE
- **Type-2 Hypervisor:** VMware Workstation

Both virtual machines were configured with the same basic resources to maintain a fair comparison:

| Resource | Configuration |
|---|---|
| Guest Operating System | Ubuntu |
| CPU | 2 vCPU |
| Memory | 2 GB RAM |
| Disk | 20 GB |
| Benchmark Tool | Sysbench |

The CPU performance was measured using the following Sysbench command:

```bash
sysbench cpu --cpu-max-prime=20000 run
