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

2. Type-1 Hypervisor Results – Proxmox VE
2.1 Configuration
<table> <tr> <th>Parameter</th> <th>Value</th> </tr> <tr> <td>Hypervisor</td> <td>Proxmox VE</td> </tr> <tr> <td>Hypervisor Type</td> <td>Type-1</td> </tr> <tr> <td>Guest Operating System</td> <td>Ubuntu</td> </tr> <tr> <td>CPU</td> <td>2 vCPU</td> </tr> <tr> <td>Memory</td> <td>2 GB</td> </tr> <tr> <td>Disk</td> <td>20 GB</td> </tr> <tr> <td>Network</td> <td>vmbr0</td> </tr> </table>

