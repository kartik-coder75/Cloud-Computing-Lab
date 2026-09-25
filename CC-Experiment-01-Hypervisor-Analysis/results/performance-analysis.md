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

| Parameter         | Proxmox VE | VMware Workstation | Difference |
| ----------------- | ---------: | -----------------: | ---------: |
| Execution Time    |   9.9968 s |           9.9959 s |   0.0009 s |
| Total Events      |      15877 |               6898 |       8979 |
| Events per Second |    1587.47 |             689.57 |     897.90 |
| Minimum Latency   |    0.59 ms |            1.25 ms |    0.66 ms |
| Average Latency   |    0.63 ms |            1.45 ms |    0.82 ms |
| Maximum Latency   |    1.34 ms |            4.23 ms |    2.89 ms |

