# Hypervisor Performance Analysis Report

## 🧪 Experiment 01: Proxmox VE (Type-1) vs. VMware Workstation (Type-2)

### 📋 Test Setup Summary
Both hypervisors were tested under identical hardware resource constraints to measure virtualization overhead and execution efficiency.

* **Workload**: `sysbench cpu --cpu-max-prime=20000 run`
* **vCPU Allocation**: 2 Cores
* **RAM Allocation**: 2048 MB (2 GB)
* **Storage Allocation**: 20 GB

---

## 📊 Benchmark Results Table

| Parameter / Metric | Type-1 Hypervisor (Proxmox VE) | Type-2 Hypervisor (VMware Workstation) |
| :--- | :--- | :--- |
| **Hypervisor Type** | Bare-Metal (Type-1) | Hosted (Type-2) |
| **Guest OS** | Ubuntu 22.04 LTS | Ubuntu 22.04 LTS |
| **Allocated vCPU** | 2 vCPUs | 2 vCPUs |
| **Allocated Memory** | 2 GB RAM | 2 GB RAM |
| **Allocated Disk** | 20 GB | 20 GB |
| **Total Execution Time (s)** | *(Record value from sysbench)* | *(Record value from sysbench)* |
| **Total Number of Events** | *(Record value from sysbench)* | *(Record value from sysbench)* |
| **Events Per Second (EPS)** | *(Record value from sysbench)* | *(Record value from sysbench)* |
| **Average Latency (ms)** | *(Record value from sysbench)* | *(Record value from sysbench)* |
| **Minimum Latency (ms)** | *(Record value from sysbench)* | *(Record value from sysbench)* |
| **Maximum Latency (ms)** | *(Record value from sysbench)* | *(Record value from sysbench)* |

---

## 💡 Key Analysis & Observations
1. **Virtualization Overhead**:
   - **Type-1 Hypervisor (Proxmox VE)** runs directly on host hardware without an underlying OS layer, reducing virtualization latency and CPU overhead.
   - **Type-2 Hypervisor (VMware Workstation)** operates on top of the host operating system (Windows/Linux), introducing host OS scheduling context switching overhead.

2. **Execution Speed & Throughput**:
   - Higher **Events Per Second (EPS)** indicates superior CPU processing throughput.
   - Lower **Total Execution Time** and **Average Latency** demonstrate lower virtualization latency.

---

## 📷 Screenshots Evidence
- Type-1 Proxmox Screenshots: `../screenshots/type1-proxmox/`
- Type-2 VMware Screenshots: `../screenshots/type2-vmware/`
- Comparison Table Screenshot: `../screenshots/comparison/01-hypervisor-performance-comparison.png`
