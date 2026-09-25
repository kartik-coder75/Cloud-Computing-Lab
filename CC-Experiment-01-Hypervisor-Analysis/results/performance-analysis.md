# Performance Analysis

## 1. Overview and Environment Setup

This document presents the empirical benchmark results comparing the performance of a **Type-1 Bare-Metal Hypervisor (Proxmox VE)** and a **Type-2 Hosted Hypervisor (VMware Workstation)**. Both virtual machines were provisioned with identical hardware resources and ran Ubuntu as the guest operating system. CPU performance and latency were measured using **Sysbench**.

### Virtual Machine Resource Specification

| Resource | Type-1 (Proxmox VE) | Type-2 (VMware Workstation) |
| :--- | :--- | :--- |
| **Guest OS** | Ubuntu 22.04 LTS | Ubuntu 22.04 LTS |
| **vCPU** | 2 vCPU (1 Socket, 2 Cores) | 2 vCPU (1 Processor, 2 Cores) |
| **RAM** | 2048 MiB (~2 GB) | 2048 MB (~2 GB) |
| **Disk Size** | 20 GB | 20 GB |
| **Network Interface** | Bridge (`vmbr0`) | NAT |
| **Benchmark Tool** | Sysbench (`--cpu-max-prime=20000`) | Sysbench (`--cpu-max-prime=20000`) |

---

## 2. Benchmark Results & Data Comparison

The benchmark was executed using the command:
```bash
sysbench cpu --cpu-max-prime=20000 run

```
---
## 3. Performance Difference Summary

| Parameter |	Proxmox VE | VMware Workstation |	Difference |
| Execution Time |	9.9968 s	9.9959 s	0.0009 s
| Total Events |	15877 |	6898 |	8979 |
| Events per Second |	1587.47	| 689.57 | 897.90 |
| Minimum Latency |	0.59 ms	| 1.25 ms |	0.66 ms |
| Average Latency |	0.63 ms	| 1.45 ms |	0.82 ms |
| Maximum Latency |	1.34 ms	| 4.23 ms |	2.89 ms |
