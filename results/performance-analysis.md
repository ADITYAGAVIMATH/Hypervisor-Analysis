# Hypervisor Performance Analysis Report
## Experiment 01: Proxmox VE (Type-1) vs. VMware Workstation (Type-2)

---

## 1. Test Environment Summary

* **Benchmark Workload**: `sysbench cpu --cpu-max-prime=20000 run`
* **Virtual CPU (vCPU)**: 2 Cores (1 Socket × 2 Cores)
* **Allocated RAM**: 2048 MB (2.0 GB)
* **Virtual Storage**: 20.0 GB
* **Guest OS**: Ubuntu 22.04 LTS (64-bit)

---

## 2. Quantitative Results Comparison

| Parameter / Metric | Type-1 Hypervisor (Proxmox VE) | Type-2 Hypervisor (VMware Workstation) | Impact / Note |
| :--- | :--- | :--- | :--- |
| **Architecture** | Bare-Metal | Hosted (Windows Host) | Direct hardware vs Host OS layer |
| **Total Execution Time** | *(Pending Test Run)* | **10.0011 s** | Benchmark duration |
| **Total Events** | *(Pending Test Run)* | **6,213** | Higher is better |
| **Events Per Second (EPS)** | *(Pending Test Run)* | **621.07** | **Main Throughput Metric** (Higher is better) |
| **Average Latency** | *(Pending Test Run)* | **1.61 ms** | Lower is better |
| **Minimum Latency** | *(Pending Test Run)* | **1.52 ms** | Lowest latency recorded |
| **Maximum Latency** | *(Pending Test Run)* | **4.77 ms** | Peak latency spike |

---

## 3. Analysis & Key Takeaways

1. **Virtualization Overhead**:
   - Proxmox VE operates directly on bare-metal hardware using the KVM kernel module. This provides direct hardware-assisted virtualization (Intel VT-x / AMD-V) with minimal latency.
   - VMware Workstation operates on top of a host operating system (Windows/Linux), introducing scheduling contention between guest vCPU threads and background host processes.

2. **Conclusion**:
   - For enterprise servers, multi-tenant cloud platforms, and production workloads, Type-1 hypervisors offer lower overhead and higher deterministic throughput.
   - For local development and educational labs, Type-2 hypervisors provide convenience and flexibility without requiring dedicated physical server hardware.

---

## 4. Screenshot References

* **Proxmox VE (Type-1)**:
  - Web Dashboard: `../screenshots/type1-proxmox/01-proxmox-dashboard.png`
  - Additional captures pending hardware testing.
* **VMware Workstation (Type-2)**:
  - Hardware Settings: `../screenshots/type2-vmware/01-vmware-vm-configuration.png`
  - Running VM: `../screenshots/type2-vmware/02-vmware-vm-running.png`
  - System Verification: `../screenshots/type2-vmware/03-vmware-system-configuration.png`
  - Sysbench Benchmark Result: `../screenshots/type2-vmware/04-vmware-sysbench-result.png`
