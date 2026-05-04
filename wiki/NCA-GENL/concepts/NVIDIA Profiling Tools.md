---
tags: [concept, nvidia, profiling, tooling, deployment]
exam: NCA-GENL
domain: Deployment and Optimization
---

# NVIDIA Profiling and Management Tools

NVIDIA provides a layered set of tools for monitoring, profiling, and managing GPU hardware — from single-developer debugging to enterprise data center operations.

---

## Tool Hierarchy

| Scope | Tool | Primary Use |
|---|---|---|
| Code-level kernel | Nsight Compute | Micro-optimize individual CUDA kernels |
| System-level | Nsight Systems | Identify CPU/GPU bottlenecks across the whole app |
| Single-node monitoring | nvidia-smi | Quick GPU health check, utilization, memory |
| Data center / cluster | NVIDIA DCGM | Cluster-wide GPU health, metrics, alerts |
| NVLink fabric | Fabric Manager | Initialize & monitor multi-GPU NVLink topology |
| Cluster lifecycle | Base Command Manager | OS deployment, cluster provisioning, management |

---

## Nsight Suite

### Nsight Systems
- **Scope:** System-wide — CPU + GPU + OS + network interactions.
- **What it shows:** Timeline of all CPU threads, GPU streams, CUDA API calls, memory transfers.
- **Use case:** Find macro-level bottlenecks:
  - GPU idle while CPU prepares data (data loading bottleneck)
  - Memory copy stalls
  - Poor overlap between compute and I/O

### Nsight Compute
- **Scope:** Single CUDA kernel — deep hardware counter analysis.
- **What it shows:** Memory access patterns, occupancy, warp stalls, compute unit utilization, cache hit rates.
- **Use case:** Code-level optimization after Nsight Systems identifies the hot kernel.

**Workflow:** Use Nsight Systems first to find *which* kernel is slow → then Nsight Compute to understand *why*.

---

## nvidia-smi

**NVIDIA System Management Interface** — the essential command-line tool.

```bash
nvidia-smi          # snapshot of all GPUs
nvidia-smi -l 1     # refresh every second
nvidia-smi dmon     # per-GPU streaming metrics
```

| Metric | Command |
|---|---|
| GPU utilization (%) | `nvidia-smi` → `GPU-Util` column |
| Memory used/total | `nvidia-smi` → `Memory-Usage` column |
| Power draw | `nvidia-smi` → `Power` column |
| Running processes | `nvidia-smi` → `Processes` section |
| Temperature | `nvidia-smi` → `Temp` column |

- Available on any NVIDIA GPU system.
- First tool to check when debugging GPU issues.

---

## NVIDIA DCGM (Data Center GPU Manager)

DCGM = enterprise/cluster-grade version of nvidia-smi.

| Feature | nvidia-smi | DCGM |
|---|---|---|
| Scope | Single node, manual | Multi-node cluster, automated |
| Health checks | Basic | Proactive diagnostics (GPU, NVLink, PCIe) |
| Metrics | Snapshot | Time-series with historical retention |
| Integration | Standalone CLI | Kubernetes, Prometheus, Grafana |
| Alerting | None | Configurable alerts and policies |

- Used in DGX SuperPOD and cloud AI infrastructure.
- Integrates with **Kubernetes** via the DCGM Exporter for Prometheus-based monitoring.

---

## NVIDIA Fabric Manager

- Configures and monitors the **NVLink fabric** (interconnect mesh) in multi-GPU systems (DGX).
- Runs as a daemon; **must be running** for NVLink/NVSwitch to work correctly on DGX systems.
- Without Fabric Manager, NVLink communication fails silently or degrades.

## NVIDIA Base Command Manager

- Automates **cluster lifecycle management**: OS deployment, driver installation, health checks.
- Primarily used for managing large DGX clusters (bare-metal provisioning to software updates).

---

## Exam Notes

- Know the **two-level Nsight workflow**: Nsight Systems (macro) → Nsight Compute (micro).
- **nvidia-smi** = single GPU monitoring; **DCGM** = cluster-level enterprise monitoring.
- DCGM integrates with **Kubernetes/Prometheus** for cloud-native GPU observability.
- **Fabric Manager** must be running for NVLink to initialize on DGX systems.

---

## Related

- [[NVIDIA Compute Systems]]
- [[NVIDIA Ecosystem]]
- [[GPU Architecture and Hardware]]
- [[Distributed Deep Learning]]
