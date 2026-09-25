# Cloud-Computing-Lab
Lab Experiments

# Performance Analysis of Type-1 and Type-2 Hypervisors

## Proxmox VE (Type-1) vs VMware Workstation (Type-2)

This project demonstrates the creation, configuration, and performance analysis of virtual machines using two different types of hypervisors:

* **Type-1 Hypervisor:** Proxmox VE
* **Type-2 Hypervisor:** VMware Workstation

Both virtual machines are configured with the same basic resources so that their CPU performance can be measured and compared using **Sysbench**.

---

## 1. Objective

The main objectives of this experiment are:

1. To understand the working of Type-1 and Type-2 hypervisors.
2. To create a virtual machine using **Proxmox VE**.
3. To create a virtual machine using **VMware Workstation**.
4. To configure both virtual machines with similar hardware resources.
5. To install Ubuntu on both virtual machines.
6. To verify CPU, memory, disk, and system configurations.
7. To perform CPU benchmarking using Sysbench.
8. To record execution time, events per second, and latency.
9. To monitor resource utilization.
10. To compare the performance of Type-1 and Type-2 virtualization.

---

# 2. Hypervisors Used

## Type-1 Hypervisor – Proxmox VE

Proxmox VE is used as the **Type-1 hypervisor**. It runs directly on the physical server hardware and provides a web-based interface for managing virtual machines.

The virtual machine used in this experiment is configured with:

| Resource        | Configuration |
| --------------- | ------------- |
| Hypervisor      | Proxmox VE    |
| Hypervisor Type | Type-1        |
| Guest OS        | Ubuntu        |
| CPU             | 2 vCPU        |
| RAM             | 2 GB          |
| Disk            | 20 GB         |
| Network         | vmbr0         |

---

## Type-2 Hypervisor – VMware Workstation

VMware Workstation is used as the **Type-2 hypervisor**. It runs on top of a host operating system and provides an environment for creating and running virtual machines.

The virtual machine is configured with:

| Resource        | Configuration      |
| --------------- | ------------------ |
| Hypervisor      | VMware Workstation |
| Hypervisor Type | Type-2             |
| Guest OS        | Ubuntu             |
| CPU             | 2 vCPU             |
| RAM             | 2 GB               |
| Disk            | 20 GB              |
| Network         | NAT                |

The same CPU, memory, and disk configuration is used as far as possible to make the performance comparison meaningful.

---

# 3. Software and Requirements

The following are required:

* Proxmox VE
* VMware Workstation
* Ubuntu ISO image
* Web browser
* Internet/network connectivity
* Sysbench
* A system capable of running virtualization

For the Proxmox setup, access to the Proxmox server IP address and valid login credentials are required.

---

# 4. Type-1 Hypervisor – Proxmox VE

## 4.1 Accessing the Proxmox VE Web Interface

Proxmox VE is managed through a web-based interface.

### Steps

1. Connect the system to the network where the Proxmox VE server is accessible.
2. Open a web browser.
3. Enter the following address:

```text
https://<PROXMOX_SERVER_IP>:8006
```

Example:

```text
https://192.168.X.X:8006
```

4. Press **Enter**.

The Proxmox VE login page should appear.

> **Note:** The actual Proxmox server IP address and login credentials must be available before starting.

---

## 4.2 Handling the Security Warning

When opening the Proxmox web interface for the first time, the browser may show a security warning because Proxmox commonly uses a self-signed SSL certificate.

### Steps

1. Click **Advanced**.
2. Select **Proceed to <Server IP>**.
3. The Proxmox VE login page will be displayed.

---

## 4.3 Logging in to Proxmox VE

Enter the assigned login credentials.

| Parameter | Value                |
| --------- | -------------------- |
| Username  | Provided credentials |
| Password  | Provided credentials |
| Realm     | As configured        |

Click **Login**.

After successful authentication, the Proxmox VE dashboard will be displayed.

---

# 5. Understanding the Proxmox Interface

The left-side navigation panel contains the infrastructure hierarchy.

```text
Datacenter
│
├── Proxmox Node
│
├── Virtual Machines
│
├── Storage
│
└── Network
```

The Proxmox interface provides access to:

* Datacenter resources
* Proxmox server node
* Virtual machines
* Storage
* Network configuration
* CPU utilization
* Memory utilization

---

# 6. Creating the Type-1 Virtual Machine

A new virtual machine can be created using the **Create VM** wizard.

The creation process consists of:

```text
General
   ↓
OS
   ↓
System
   ↓
Disks
   ↓
CPU
   ↓
Memory
   ↓
Network
   ↓
Confirm
```

---

## 6.1 Selecting the Proxmox Node

From the left-side navigation panel:

1. Expand **Datacenter**.
2. Select the required Proxmox server node.

Example:

```text
Datacenter → pve
```

The node summary page will be displayed.

---

## 6.2 Opening the Create VM Wizard

1. Click **Create VM** in the upper-right corner.
2. The **Create: Virtual Machine** wizard will open.

---

## 6.3 Configuring General Settings

In the **General** section, configure the VM.

| Parameter | Configuration                      |
| --------- | ---------------------------------- |
| Node      | Selected Proxmox node              |
| VM ID     | Automatically assigned / allocated |
| Name      | Unique VM name                     |

Recommended naming convention:

```text
<Name>-Type1
```

Example:

```text
CC-Experiment1-Type1
```

Click **Next**.

---

# 7. Configuring the Operating System

In the **OS** section:

1. Select **Use CD/DVD Disc Image File (ISO)**.
2. Select the storage location containing the Ubuntu ISO.
3. Select the required Ubuntu ISO image.

Example:

```text
Storage: local
ISO Image: ubuntu-22.04.iso
```

Configuration:

| Parameter          | Configuration |
| ------------------ | ------------- |
| Installation Media | ISO Image     |
| Storage            | local         |
| Operating System   | Ubuntu        |

Click **Next**.

---

# 8. Configuring System Settings

The **System** section configures the virtual machine hardware platform.

Use the default settings unless otherwise specified.

| Parameter       | Configuration |
| --------------- | ------------- |
| Graphics Card   | Default       |
| Machine         | Default       |
| BIOS            | Default       |
| SCSI Controller | Default       |

Click **Next**.

---

# 9. Configuring the Virtual Disk

The **Disks** section is used to configure virtual storage.

Configure:

| Parameter  | Configuration                |
| ---------- | ---------------------------- |
| Storage    | local-lvm / assigned storage |
| Disk Size  | 20 GB                        |
| Bus/Device | Default                      |

Click **Next**.

---

# 10. Configuring CPU Resources

The CPU section controls the virtual processor resources assigned to the VM.

Configure:

| Parameter | Value |
| --------- | ----: |
| Sockets   |     1 |
| Cores     |     2 |

Therefore:

```text
Total vCPU = 1 × 2 = 2 vCPU
```

Click **Next**.

---

# 11. Configuring Memory

Configure the memory allocation as:

| Parameter |    Value |
| --------- | -------: |
| Memory    | 2048 MiB |

This is approximately:

```text
2048 MiB = 2 GB RAM
```

Click **Next**.

---

# 12. Configuring Network

Configure the virtual network interface.

| Parameter | Configuration    |
| --------- | ---------------- |
| Bridge    | vmbr0            |
| Model     | Default / VirtIO |

The `vmbr0` bridge connects the virtual machine to the configured network.

Click **Next**.

---

# 13. Confirming the Type-1 VM Configuration

Review the complete configuration before creating the VM.

| Resource         | Configuration        |
| ---------------- | -------------------- |
| VM Name          | CC-Experiment1-Type1 |
| Operating System | Ubuntu               |
| CPU              | 2 vCPU               |
| Memory           | 2 GB                 |
| Disk             | 20 GB                |
| Network          | vmbr0                |

Click **Finish**.

The virtual machine will be created.

---

# 14. Starting the Proxmox VM

After the VM is created:

1. Locate the VM in the left-side navigation panel.
2. Select the VM.
3. Click **Start** in the upper-right corner.

The VM status should change from:

```text
Stopped
```

to:

```text
Running
```

---

# 15. Opening the VM Console

After starting the VM:

1. Select the virtual machine.
2. Select **Console**.
3. The virtual machine display will open in the browser.

The Ubuntu installation interface will appear.

---

# 16. Installing Ubuntu on Proxmox VM

Complete the Ubuntu installation.

### Steps

1. Select the required language.
2. Select **Install Ubuntu**.
3. Configure the keyboard layout.
4. Select the required installation type.
5. Select the virtual disk.
6. Configure the timezone.
7. Create the Ubuntu user account.
8. Complete the installation.
9. Restart the virtual machine.
10. Log in to Ubuntu.

---

# 17. Verifying the Type-1 VM

Open the Ubuntu terminal.

Run:

```bash
hostnamectl
```

Check:

* Hostname
* Operating system
* Kernel version
* Architecture

---

## 17.1 Checking CPU Configuration

Run:

```bash
lscpu
```

Observe:

* Architecture
* Number of CPUs
* CPU model
* Virtualization information

Record the output for later comparison.

---

## 17.2 Checking Memory

Run:

```bash
free -h
```

Observe:

* Total memory
* Used memory
* Free memory
* Available memory

The allocated memory should be approximately 2 GB.

---

## 17.3 Checking Disk

Run:

```bash
df -h
```

Observe:

* Filesystem
* Total disk capacity
* Used disk space
* Available disk space

---

## 17.4 Monitoring System Resources

Run:

```bash
top
```

Observe:

* CPU utilization
* Memory utilization
* Running processes
* Load average

To exit the `top` interface, press:

```text
q
```

---

# 18. Installing Sysbench on Type-1 VM

Sysbench is used for CPU performance analysis.

First update the package repository:

```bash
sudo apt update
```

Install Sysbench:

```bash
sudo apt install sysbench -y
```

Verify the installation:

```bash
sysbench --version
```

The installed Sysbench version should be displayed.

---

# 19. Running CPU Benchmark on Proxmox

Run the CPU benchmark:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

Allow the benchmark to complete.

Record the following values from the output:

* Total execution time
* Total number of events
* Events per second
* Minimum latency
* Average latency
* Maximum latency

The benchmark result should be saved for comparison with the Type-2 VM.

---

# 20. Type-1 Performance Observation

Record the obtained results.

| Parameter            | Observation   |
| -------------------- | ------------- |
| Hypervisor           | Proxmox VE    |
| Hypervisor Type      | Type-1        |
| Guest OS             | Ubuntu        |
| CPU                  | 2 vCPU        |
| Memory               | 2 GB          |
| Disk                 | 20 GB         |
| Total Execution Time | Record result |
| Total Events         | Record result |
| Events per Second    | Record result |
| Average Latency      | Record result |

> Replace the result fields with the actual values obtained from Sysbench.

---

# 21. Monitoring Proxmox VM Resources

Return to the Proxmox VE web interface.

Navigate to:

```text
Datacenter
   → Proxmox Node
      → Virtual Machine
         → Summary
```

Observe:

* CPU usage
* Memory usage
* Network traffic
* Disk usage

Record the observations for comparison with VMware Workstation.

---

# 22. Shutting Down the Type-1 VM

After completing the analysis, shut down the Ubuntu VM properly.

Inside the Ubuntu terminal, execute:

```bash
sudo poweroff
```

Alternatively, use the shutdown option provided by the Proxmox VE interface.

Verify that the VM status changes to:

```text
Stopped
```

---

# 23. Type-2 Hypervisor – VMware Workstation

VMware Workstation is used as the **Type-2 hypervisor**.

Unlike a Type-1 hypervisor, VMware Workstation runs on top of an existing host operating system.

The VMware VM should use the same basic resources as the Proxmox VM:

```text
CPU  = 2 vCPU
RAM  = 2 GB
Disk = 20 GB
OS   = Ubuntu
```

---

# 24. Launching VMware Workstation

1. Open **VMware Workstation** from the installed applications.
2. The VMware Workstation home interface will appear.
3. Select:

```text
Create a New Virtual Machine
```

The **New Virtual Machine Wizard** will open.

---

# 25. Selecting VM Configuration

The wizard provides options such as:

* Typical (recommended)
* Custom (advanced)

Select:

```text
Typical (recommended)
```

Click **Next**.

---

# 26. Selecting Ubuntu ISO

The installation media options will be displayed.

Select:

```text
Installer disc image file (iso)
```

Click **Browse**.

Navigate to the location of the Ubuntu ISO file.

Select:

```text
ubuntu-22.04.iso
```

Click **Next**.

---

# 27. Selecting the Guest Operating System

If VMware automatically detects Ubuntu, verify the configuration.

Otherwise configure:

| Parameter              | Configuration |
| ---------------------- | ------------- |
| Guest Operating System | Linux         |
| Version                | Ubuntu 64-bit |

Click **Next**.

---

# 28. Naming the Type-2 Virtual Machine

Enter the VM name.

Recommended name:

```text
CC-Experiment1-Type2
```

Select the location where the virtual machine files should be stored.

Click **Next**.

---

# 29. Configuring Virtual Disk

Configure the virtual disk:

| Parameter         | Configuration                                 |
| ----------------- | --------------------------------------------- |
| Maximum Disk Size | 20 GB                                         |
| Disk Storage      | Store virtual disk as a single file / default |

Click **Next**.

The VM configuration summary will appear.

Before completing the VM creation, select:

```text
Customize Hardware
```

---

# 30. Configuring VMware Hardware

The **Virtual Machine Settings** window will open.

The following hardware resources need to be configured.

---

## 30.1 Configuring Memory

Select:

```text
Memory
```

Set:

```text
2048 MB
```

This is approximately:

```text
2 GB RAM
```

---

## 30.2 Configuring Processor

Select:

```text
Processors
```

Configure:

| Parameter                     | Value |
| ----------------------------- | ----: |
| Number of Processors          |     1 |
| Number of Cores per Processor |     2 |

Therefore:

```text
Total Virtual CPUs = 1 × 2 = 2 vCPU
```

---

## 30.3 Verifying Hard Disk

Select:

```text
Hard Disk
```

Verify that the disk size is:

```text
20 GB
```

---

## 30.4 Configuring Network Adapter

Select:

```text
Network Adapter
```

For this experiment, use:

```text
NAT
```

NAT allows the virtual machine to access the network through the host system.

The network configuration can be changed depending on the available environment.

---

## 30.5 Final VMware Hardware Configuration

Before closing the hardware settings, verify:

| Resource  | Configuration |
| --------- | ------------- |
| Memory    | 2 GB          |
| CPU       | 2 vCPU        |
| Hard Disk | 20 GB         |
| Network   | NAT           |
| Guest OS  | Ubuntu        |

Click **Close**.

---

# 31. Completing VMware VM Creation

The New Virtual Machine Wizard will be displayed again.

Review the complete configuration.

Click:

```text
Finish
```

The newly created VM will appear in the VMware Workstation library.

---

# 32. Starting the VMware VM

1. Select `CC-Experiment1-Type2` from the VMware Workstation library.
2. Click:

```text
Power on this virtual machine
```

The Ubuntu installation process will begin.

---

# 33. Installing Ubuntu on VMware

The Ubuntu installation interface will appear inside the VMware virtual machine.

## Step 1: Select Language

Select the required language.

Click:

```text
Install Ubuntu
```

---

## Step 2: Configure Keyboard

Select the appropriate keyboard layout.

Click:

```text
Continue
```

---

## Step 3: Select Installation Type

For a standard installation, select:

```text
Normal Installation
```

Click:

```text
Continue
```

---

## Step 4: Configure Installation Disk

Select:

```text
Erase disk and install Ubuntu
```

> This operation affects only the virtual hard disk created for the VMware virtual machine.

Click:

```text
Install Now
```

Confirm the disk changes if prompted.

---

## Step 5: Configure Time Zone

Select the appropriate geographical location and timezone.

Click:

```text
Continue
```

---

## Step 6: Create User Account

Create the Ubuntu account.

Configure:

| Parameter     | Example         |
| ------------- | --------------- |
| Name          | Your Name       |
| Computer Name | cc-type2-vm     |
| Username      | Your Username   |
| Password      | Secure Password |

Click:

```text
Continue
```

Ubuntu installation will begin.

---

# 34. Restarting VMware VM

After the installation is completed:

1. Select **Restart Now**.
2. Allow the VM to restart.
3. Log in using the Ubuntu username and password created during installation.

---

# 35. Verifying VMware VM Configuration

Open the Ubuntu Terminal.

Run:

```bash
hostnamectl
```

Verify:

* Hostname
* Operating system
* Kernel version
* Architecture

---

# 36. Checking CPU Configuration

Run:

```bash
lscpu
```

Observe:

* Architecture
* CPU(s)
* CPU model
* Number of cores
* Virtualization type

Verify that the VM has approximately:

```text
2 Virtual CPUs
```

---

# 37. Checking Memory Configuration

Run:

```bash
free -h
```

Observe:

* Total memory
* Used memory
* Free memory
* Available memory

Verify that the allocated memory is approximately:

```text
2 GB
```

---

# 38. Checking Disk Configuration

Run:

```bash
df -h
```

Observe:

* Filesystem
* Total disk capacity
* Used disk space
* Available disk space

Verify the virtual disk configuration.

---

# 39. Monitoring VMware VM Resources

Run:

```bash
top
```

Observe:

* CPU utilization
* Memory utilization
* Running processes
* Load average

Press:

```text
q
```

to exit.

---

# 40. Installing Sysbench on VMware VM

Update the package repository:

```bash
sudo apt update
```

Install Sysbench:

```bash
sudo apt install sysbench -y
```

Verify the installation:

```bash
sysbench --version
```

---

# 41. Running CPU Benchmark on VMware

Run:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

Allow the benchmark to complete.

Record:

* Total execution time
* Total number of events
* Events per second
* Minimum latency
* Average latency
* Maximum latency

---

# 42. Type-2 Performance Observation

Record the actual benchmark results.

| Parameter            | Observation        |
| -------------------- | ------------------ |
| Hypervisor           | VMware Workstation |
| Hypervisor Type      | Type-2             |
| Guest OS             | Ubuntu             |
| CPU                  | 2 vCPU             |
| Memory               | 2 GB               |
| Disk                 | 20 GB              |
| Total Execution Time | Record result      |
| Total Events         | Record result      |
| Events per Second    | Record result      |
| Minimum Latency      | Record result      |
| Average Latency      | Record result      |
| Maximum Latency      | Record result      |

---

# 43. Monitoring VMware Resource Utilization

Return to VMware Workstation.

Select the running virtual machine.

The configured hardware can be viewed through:

```text
VM → Settings
```

Verify:

* Processors
* Memory
* Hard Disk
* Network Adapter

Additional resource information can be monitored inside Ubuntu using:

```bash
top
```

or:

```bash
free -h
```

---

# 44. Final Type-2 Results

Record the final Sysbench results.

| Performance Metric   | Result             |
| -------------------- | ------------------ |
| Hypervisor           | VMware Workstation |
| Hypervisor Type      | Type-2             |
| CPU Configuration    | 2 vCPU             |
| Memory Configuration | 2 GB               |
| Disk Configuration   | 20 GB              |
| Total Execution Time | Record result      |
| Total Events         | Record result      |
| Events per Second    | Record result      |
| Minimum Latency      | Record result      |
| Average Latency      | Record result      |
| Maximum Latency      | Record result      |

---

# 45. Comparison of Type-1 and Type-2 Hypervisors

After running the same Sysbench benchmark on both virtual machines, record the results in a common table.

| Parameter            | Proxmox VE    | VMware Workstation |
| -------------------- | ------------- | ------------------ |
| Hypervisor Type      | Type-1        | Type-2             |
| Guest OS             | Ubuntu        | Ubuntu             |
| CPU                  | 2 vCPU        | 2 vCPU             |
| Memory               | 2 GB          | 2 GB               |
| Disk                 | 20 GB         | 20 GB              |
| Network              | vmbr0         | NAT                |
| Total Execution Time | Record result | Record result      |
| Total Events         | Record result | Record result      |
| Events per Second    | Record result | Record result      |
| Minimum Latency      | Record result | Record result      |
| Average Latency      | Record result | Record result      |
| Maximum Latency      | Record result | Record result      |

---

# 46. Understanding the Performance Metrics

## Total Execution Time

This represents the total amount of time required by Sysbench to complete the benchmark.

```text
Lower execution time → faster completion
```

---

## Total Events

This represents the total number of benchmark operations performed during the test.

---

## Events Per Second

This represents the number of benchmark operations completed per second.

```text
Higher events/second → higher benchmark throughput
```

---

## Latency

Latency represents the time taken to complete an individual operation.

The benchmark may report:

* Minimum latency
* Average latency
* Maximum latency

Lower latency indicates that individual operations are being completed in less time.

---

# 47. Performance Analysis

The benchmark results from both hypervisors can be analyzed using:

### CPU Performance

Compare:

```text
Total Execution Time
Events Per Second
```

### Response Time

Compare:

```text
Average Latency
Minimum Latency
Maximum Latency
```

### Resource Utilization

Compare:

```text
CPU Usage
Memory Usage
Disk Usage
Network Usage
```

The actual conclusion should be based on the measured values obtained during the experiment.

---

# 48. Type-1 Hypervisor Workflow

```text
Access Proxmox VE
        ↓
Login to Proxmox
        ↓
Select Proxmox Node
        ↓
Create Virtual Machine
        ↓
Select Ubuntu ISO
        ↓
Configure 20 GB Disk
        ↓
Configure 2 vCPU
        ↓
Configure 2 GB RAM
        ↓
Configure vmbr0 Network
        ↓
Create VM
        ↓
Start VM
        ↓
Install Ubuntu
        ↓
Verify CPU, Memory and Disk
        ↓
Install Sysbench
        ↓
Run CPU Benchmark
        ↓
Record Results
        ↓
Monitor Resources
        ↓
Shutdown VM
```

---

# 49. Type-2 Hypervisor Workflow

```text
Launch VMware Workstation
        ↓
Create New Virtual Machine
        ↓
Select Typical Configuration
        ↓
Select Ubuntu ISO
        ↓
Configure VM Name and Location
        ↓
Configure 20 GB Disk
        ↓
Customize Hardware
        ↓
Configure 2 vCPU
        ↓
Configure 2 GB RAM
        ↓
Configure NAT Network
        ↓
Finish VM Creation
        ↓
Power On VM
        ↓
Install Ubuntu
        ↓
Verify CPU, Memory and Disk
        ↓
Install Sysbench
        ↓
Run CPU Benchmark
        ↓
Record Results
        ↓
Monitor Resources
        ↓
Shutdown VM
```

---

# 50. Important Commands Used

## System Information

```bash
hostnamectl
```

## CPU Information

```bash
lscpu
```

## Memory Information

```bash
free -h
```

## Disk Information

```bash
df -h
```

## Resource Monitoring

```bash
top
```

Press `q` to exit.

## Update Ubuntu Packages

```bash
sudo apt update
```

## Install Sysbench

```bash
sudo apt install sysbench -y
```

## Check Sysbench Version

```bash
sysbench --version
```

## CPU Benchmark

```bash
sysbench cpu --cpu-max-prime=20000 run
```

## Shutdown Ubuntu VM

```bash
sudo poweroff
```

---

# 51. Expected Outcome

After completing the experiment, two Ubuntu virtual machines will have been created:

```text
Proxmox VE
   └── Ubuntu VM
       ├── 2 vCPU
       ├── 2 GB RAM
       └── 20 GB Disk

VMware Workstation
   └── Ubuntu VM
       ├── 2 vCPU
       ├── 2 GB RAM
       └── 20 GB Disk
```

Sysbench CPU benchmarking is then used to obtain performance measurements from both environments.

The collected results can be used to compare:

* CPU execution time
* Number of benchmark events
* Events per second
* Latency
* CPU utilization
* Memory utilization
* Overall virtualization behavior

---

# 52. Final Comparison

The experiment provides a practical comparison between:

```text
Type-1 Hypervisor
       │
       ▼
   Proxmox VE
       │
       ▼
 Ubuntu Virtual Machine


Type-2 Hypervisor
       │
       ▼
VMware Workstation
       │
       ▼
 Ubuntu Virtual Machine
```

Both environments use approximately the same virtual hardware configuration and the same Ubuntu guest operating system. Sysbench is used to perform the CPU benchmark under both virtualization environments.

The final performance comparison should be based on the actual benchmark values recorded during execution rather than assumed values.

---

# 53. Conclusion

This experiment demonstrates the practical setup and performance analysis of two different virtualization approaches.

**Proxmox VE** is used as the Type-1 hypervisor, where virtualization is provided directly on the physical server platform. **VMware Workstation** is used as the Type-2 hypervisor, where virtualization operates through the host operating system.

Both virtual machines are configured with:

* Ubuntu operating system
* 2 virtual CPUs
* 2 GB RAM
* 20 GB virtual disk

After configuring both environments, system information is verified using Linux commands and CPU performance is measured using Sysbench.

The recorded execution time, events per second, and latency values provide the basis for comparing the two virtualization environments.

---

## Repository Structure

A suggested repository structure is:

```text
Hypervisor-Performance-Analysis/
│
├── README.md
│
├── Type-1-Proxmox/
│   ├── screenshots/
│   └── results/
│
├── Type-2-VMware/
│   ├── screenshots/
│   └── results/
│
└── comparison/
    └── performance-results.md
```

Screenshots of the Proxmox interface, VMware Workstation, Ubuntu terminal outputs, Sysbench results, and final comparison can be added to the respective folders.

---

## Technologies Used

* **Proxmox VE**
* **VMware Workstation**
* **Ubuntu Linux**
* **Sysbench**
* **Virtualization**
* **CPU Benchmarking**

---

## Key Commands

```bash
hostnamectl
lscpu
free -h
df -h
top
sudo apt update
sudo apt install sysbench -y
sysbench --version
sysbench cpu --cpu-max-prime=20000 run
sudo poweroff
```

---

## Experiment Summary

| Feature             | Type-1          | Type-2             |
| ------------------- | --------------- | ------------------ |
| Hypervisor          | Proxmox VE      | VMware Workstation |
| Hypervisor Category | Type-1          | Type-2             |
| Guest OS            | Ubuntu          | Ubuntu             |
| CPU                 | 2 vCPU          | 2 vCPU             |
| RAM                 | 2 GB            | 2 GB               |
| Disk                | 20 GB           | 20 GB              |
| Network             | vmbr0           | NAT                |
| Benchmark           | Sysbench        | Sysbench           |
| Main Analysis       | CPU Performance | CPU Performance    |

---

**Note:** The performance values in the comparison tables should be replaced with the actual values obtained when running the Sysbench benchmark on your systems.
