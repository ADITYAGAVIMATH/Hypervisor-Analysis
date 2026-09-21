# Experiment 01: Performance Analysis of Type-1 and Type-2 Hypervisors

## 📌 Overview
This repository contains the complete experimental setup, procedure, benchmark results, and analysis for **Experiment 01: Performance Analysis of Type-1 (Proxmox VE) and Type-2 (VMware Workstation) Hypervisors**. 

The goal of this experiment is to deploy identically configured Ubuntu Virtual Machines (VMs) on both hypervisor architectures and compare their performance using the **Sysbench** CPU benchmarking tool.

---

## 💻 Hardware & Software Requirements

| Component | Requirement / Tool |
| :--- | :--- |
| **Type-1 Hypervisor** | Proxmox VE (Web Interface on `https://<PROXMOX_SERVER_IP>:8006`) |
| **Type-2 Hypervisor** | VMware Workstation Pro / Player |
| **Guest OS** | Ubuntu 22.04 LTS Desktop / Server ISO |
| **Benchmark Tool** | `sysbench` |
| **Version Control** | Git & GitHub |

---

## ⚙️ Standard Virtual Machine Configuration
To ensure a fair performance comparison, identical hardware resource limits were allocated to both virtual machines:

| Parameter | Configuration |
| :--- | :--- |
| **Guest OS** | Ubuntu 22.04 LTS (64-bit) |
| **Virtual CPUs (vCPU)** | 2 vCPUs |
| **Memory (RAM)** | 2048 MB (2 GB) |
| **Storage (Disk)** | 20 GB |
| **Network Adapter** | NAT |
| **Benchmark Command** | `sysbench cpu --cpu-max-prime=20000 run` |

---

## 📂 Repository Directory Structure

```text
CC-Experiment-01-Hypervisor-Analysis/
│
├── screenshots/
│   ├── type1-proxmox/
│   │   ├── 01-proxmox-dashboard.png
│   │   ├── 02-proxmox-vm-configuration.png
│   │   ├── 03-proxmox-vm-running.png
│   │   ├── 04-proxmox-ubuntu-console.png
│   │   ├── 05-proxmox-system-configuration.png
│   │   ├── 06-proxmox-sysbench-result.png
│   │   └── 07-proxmox-resource-monitoring.png
│   │
│   ├── type2-vmware/
│   │   ├── 01-vmware-vm-configuration.png
│   │   ├── 02-vmware-vm-running.png
│   │   ├── 03-vmware-system-configuration.png
│   │   └── 04-vmware-sysbench-result.png
│   │
│   └── comparison/
│       └── 01-hypervisor-performance-comparison.png
│
├── results/
│   └── performance-analysis.md
│
└── README.md
```

---

## 🛠️ Step-by-Step Execution Procedure

### PART A: Type-1 Hypervisor (Proxmox VE)
1. **Access Web Console**: Navigate to `https://<PROXMOX_SERVER_IP>:8006` and log in with credentials.
2. **Create VM**:
   - Assign Name: `CC-Experiment1-Type1`
   - Select ISO image (`ubuntu-22.04.iso`).
   - Allocate **2 vCPUs**, **2048 MB RAM**, and **20 GB Disk**.
3. **OS Installation & System Check**:
   - Start VM and complete Ubuntu installation.
   - Open terminal and verify configuration:
     ```bash
     lscpu
     free -h
     df -h
     ```
4. **Benchmark Execution**:
   - Install Sysbench:
     ```bash
     sudo apt update && sudo apt install sysbench -y
     ```
   - Execute CPU Benchmark:
     ```bash
     sysbench cpu --cpu-max-prime=20000 run
     ```
5. **Capture Screenshots**: Save outputs into `screenshots/type1-proxmox/`.

---

### PART B: Type-2 Hypervisor (VMware Workstation)
1. **Launch VMware Workstation**: Click *Create a New Virtual Machine* -> Select *Typical*.
2. **Configure VM**:
   - Select Ubuntu ISO.
   - Set VM Name: `CC-Experiment1-Type2`.
   - Set Disk Size: **20 GB**.
   - Under *Customize Hardware*, set **Memory = 2 GB** and **Processors = 2 cores**.
3. **OS Installation & System Check**:
   - Power on VM, complete Ubuntu setup, open terminal, and run:
     ```bash
     lscpu
     free -h
     ```
4. **Benchmark Execution**:
   - Run Sysbench benchmark:
     ```bash
     sysbench cpu --cpu-max-prime=20000 run
     ```
5. **Capture Screenshots**: Save outputs into `screenshots/type2-vmware/`.

---

## 📊 Performance Benchmark Results
Detailed metrics and performance comparison table can be found in [results/performance-analysis.md](results/performance-analysis.md).

---

## 📝 Commands Summary Reference
| Purpose | Command |
| :--- | :--- |
| Check CPU Cores | `lscpu` |
| Check RAM | `free -h` |
| Check Disk Storage | `df -h` |
| Resource Utilization | `top` |
| Sysbench CPU Benchmark | `sysbench cpu --cpu-max-prime=20000 run` |
| Shutdown VM | `sudo poweroff` |
