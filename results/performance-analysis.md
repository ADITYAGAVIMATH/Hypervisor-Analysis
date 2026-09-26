# Hypervisor Performance Analysis Report

## Experiment 01: Proxmox VE (Type-1) vs. VMware Workstation (Type-2)

---

## 1. Test Environment and Workload Profile

To assess the performance differentials between bare-metal and hosted virtualization architectures, identical hardware parameters and workload suites were configured across both environments.

* **Benchmark Workload**: `sysbench cpu --cpu-max-prime=20000 run`
* **Virtual CPU (vCPU)**: 2 Cores (1 Socket x 2 Cores)
* **Allocated Memory (RAM)**: 2048 MB (2.0 GB)
* **Virtual Disk Allocation**: 20.0 GB
* **Guest Operating System**: Ubuntu 22.04 LTS (x86_64)

---

## 2. Quantitative Metric Comparison

The following table summarizes the key performance indicators collected during the execution of the CPU benchmark test suite:

| Performance Metric | Type-1 Hypervisor (Proxmox VE) | Type-2 Hypervisor (VMware Workstation) | Impact / Direction |
| :--- | :--- | :--- | :--- |
| **Hypervisor Model** | Bare-Metal (Type-1) | Hosted (Type-2) | Architecture Type |
| **Host OS Layer** | None (Direct Linux KVM Kernel) | Windows 11 / Desktop OS | Resource Intermediation |
| **Total Execution Time** | *(Pending Test Run)* | **10.0011 s** | Lower is better |
| **Total Number of Events** | *(Pending Test Run)* | **6,213** | Higher is better |
| **Events Per Second (EPS)** | *(Pending Test Run)* | **621.07** | Higher is better (Throughput) |
| **Average Latency** | *(Pending Test Run)* | **1.61 ms** | Lower is better |
| **Minimum Latency** | *(Pending Test Run)* | **1.52 ms** | Lower is better |
| **Maximum Latency** | *(Pending Test Run)* | **4.77 ms** | Lower is better |

---

## 3. Detailed Technical Analysis

### 3.1 Virtualization Overhead and CPU Scheduling
* **Proxmox VE (Type-1)**: Proxmox VE utilizes KVM (Kernel-based Virtual Machine) built directly into the Linux kernel running on bare metal. Guest vCPU threads are scheduled directly by the kernel's scheduler with direct access to hardware-assisted virtualization extensions (Intel VT-x / AMD-V), minimizing VM-exit latencies.
* **VMware Workstation (Type-2)**: The hypervisor operates as a user-level/kernel-assisted application running on top of a host operating system. Guest instructions must pass through the host OS scheduling queue, competing for hardware threads against background host tasks, anti-virus processes, and desktop window managers.

### 3.2 Memory and Address Translation (SLAT)
* Direct hardware virtualization in Type-1 hypervisors utilizes Extended Page Tables (EPT) to translate guest physical addresses directly to host physical addresses.
* In Type-2 hypervisors, memory access requires coordination with the host OS virtual memory manager, creating additional abstraction layers and potential TLB miss penalties during high computational bursts.

---

## 4. Screenshot and Experimental Evidence

### 4.1 Type-1 Hypervisor (Proxmox VE) Evidence
* Dashboard Interface: `../screenshots/type1-proxmox/01-proxmox-dashboard.png`
* Hardware Provisioning: `../screenshots/type1-proxmox/02-proxmox-vm-configuration.png` *(Pending)*
* VM Operating Session: `../screenshots/type1-proxmox/03-proxmox-vm-running.png` *(Pending)*
* Diagnostic Verification: `../screenshots/type1-proxmox/04-proxmox-system-configuration.png` *(Pending)*
* Benchmark Execution: `../screenshots/type1-proxmox/05-proxmox-sysbench-result.png` *(Pending)*

### 4.2 Type-2 Hypervisor (VMware Workstation) Evidence
* Hardware Settings: `../screenshots/type2-vmware/01-vmware-vm-configuration.png`
* VM Running Ubuntu: `../screenshots/type2-vmware/02-vmware-vm-running.png`
* Diagnostics (`hostnamectl`, `lscpu`, `free -h`, `df -h`): `../screenshots/type2-vmware/03-vmware-system-configuration.png`
* Sysbench Results: `../screenshots/type2-vmware/04-vmware-sysbench-result.png`

---

## 5. Summary Conclusion

1. **Bare-Metal Advantage**: Type-1 hypervisors deliver superior deterministic CPU throughput and reduced latency variability due to the absence of host OS intermediation.
2. **Hosted Hypervisor Utility**: Type-2 hypervisors provide convenience for software testing, educational demonstrations, and multi-OS desktop workflows where bare-metal server access is unavailable.
