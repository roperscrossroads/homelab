# Welcome to My Homelab

I like building platforms. I started work as an embedded software engineer out of college, working on large networked systems. I spent a few years creating an embedded Linux distribution for medical devices (using Yocto) and most recently I worked on building cloud infrastructure and CI/CD systems using kubernetes.

I have worked with many different large, distributed systems. I like thinking about how systems can continue to operate when some parts experience failures. I worked on fire alarm panels for a number of years which required a lot of thought about how to make things fail gracefully (while buildings are on fire).

I am building a kubernetes home lab (again) so I have a place to test things out and do research in different areas. It runs on a combination of VMs and baremetal systems (amd64 & arm64). Right now there are 11 nodes, 8 physical hosts and 68 CPU cores.

## Areas of Interest

- Self-healing systems
- Automated vulnerability detection & management
- Declarative systems
- Immutable infrastructure
- Infrastructure as code
- Container orchestration
- Observability

## Software

- **Kubernetes** for orchestration
- **Talos Linux** as the primary OS for Kubernetes
- **Ceph** (external) used for storage
- **Flux** for continuous delivery/GitOps
- **QEMU/KVM** used for running Talos VMs

## Hardware

I have set this cluster up so that some of the nodes come and go as desktop systems are turned on and off. When my daughter plays RDR2 on the gaming pc, the talos03 VM (a master node) and the talos08 VM (a worker node) are active. Likewise, my NixOS desktop runs a few worker VMs. When these systems are turned off, only the lower-power Intel N100 and Raspberry Pi4 systems remain active.

| Host    | Arch  | CPU        | Cores | RAM   | K8s Masters | K8s Workers  | Non-K8s | Notes    |
|---------|-------|------------|-------|-------|-------------|--------------|---------|----------|
| nuc1    | amd64 | Intel N100 | 4     | 16 GB | talos01     |              | ceph    |          |
| nuc2    | amd64 | Intel N100 | 4     | 16 GB | talos02     |              | ceph    |          |
| nuc3    | amd64 | Intel N100 | 4     | 16 GB |             | talos04 & 05 | ceph    |          |
| nixos   | amd64 | Ryzen 7    | 16    | 32 GB |             | talos06 & 07 |         | volatile |
| gamer   | amd64 | Intel i7   | 28    | 64 GB | talos03     | talos08      |         | volatile |
| rpi4 #1 | arm64 | Cortex-A72 | 4     | 4 GB  |             | talos09      |         |          |
| rpi4 #2 | arm64 | Cortex-A72 | 4     | 4 GB  |             | talos10      |         |          |
| rpi4 #3 | arm64 | Cortex-A72 | 4     | 8 GB  |             | talos11      |         |          |

## Nodes

| Node    | Job    | CPUs | RAM | VM?       | Notes    |
|---------|--------|------|-----|-----------|----------|
| talos01 | master | 4    | 8GB | VM        |          |
| talos02 | master | 4    | 8GB | VM        |          |
| talos03 | master | 12   | 8GB | VM        | volatile |
| talos04 | worker | 4    | 6GB | VM        |          |
| talos05 | worker | 4    | 6GB | VM        |          |
| talos06 | worker | 8    | 6GB | VM        | volatile |
| talos07 | worker | 8    | 6GB | VM        | volatile |
| talos08 | worker | 12   | 8GB | VM        | volatile |
| talos09 | worker | 4    | 4GB | baremetal |          |
| talos10 | worker | 4    | 4GB | baremetal |          |
| talos11 | worker | 4    | 8GB | baremetal |          |


## Future

There are a lot of interesting projects that I would like to explore. I am going to try to use these in some way within my homelab:

- [vcluster](https://github.com/loft-sh/vcluster) - Create fully functional virtual Kubernetes clusters
- [kcp](https://github.com/kcp-dev/kcp) - Kubernetes-like control planes for form-factors and use-cases beyond Kubernetes and container workloads
- [KubeVirt](https://github.com/kubevirt/kubevirt) - A virtual machine management add-on for Kubernetes
- [k8sgpt](https://github.com/k8sgpt-ai/k8sgpt) - A tool for scanning your Kubernetes clusters, diagnosing, and triaging issues in simple English
- [Tinkerbell](https://github.com/tinkerbell) - A flexible bare metal provisioning engine
- [NixOS](https://github.com/nixos) - Declarative builds and deployments
- [Proxmox on NixOS](https://github.com/SaumonNet/proxmox-nixos) - The Proxmox Hypervisor, on NixOS
- [KubeEdge](https://kubeedge.io/) - Kubernetes Native Edge Computing Framework
- [Kairos](https://github.com/kairos-io/kairos) - The immutable Linux meta-distribution for edge Kubernetes

## Thanks

A big thanks to [onedr0p](https://github.com/onedr0p) for his [template](https://github.com/onedr0p/cluster-template) to bootstrap the cluster. I have been watching his work for years now and it is amazing what he has done for the kubernetes/homelab community. I have [tinkered with](https://github.com/roperscrossroads/kubernetes-flux-gitops) a few iterations of his template over the years and I have learned a lot from doing so, and from looking at other repos based on his work.
