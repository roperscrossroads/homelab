# Welcome to My Homelab

I like building platforms. I started work as an embedded software engineer out of college, working on large networked systems. I spent a few years creating an embedded Linux distribution for medical devices (using Yocto) and most recently I worked on building cloud infrastructure and CI/CD systems using kubernetes.

I have worked with many different large, distributed systems. I like thinking about how systems can continue to operate when some parts experience failures. I worked on fire alarm panels for a number of years which required a lot of thought about how to make things fail gracefully (while buildings are on fire).

I am building a kubernetes home lab (again) so I have a place to test things out and do research in different areas. It runs on a combination of VMs and baremetal systems (amd64 & arm64). Right now there are 10 nodes, 7 physical hosts and 64 CPU cores.

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

| Host  | Arch  | CPU         | Cores | RAM   | K8s Masters | K8s Workers      | Non-K8s | Notes |
|-------|-------|-------------|-------|-------|-------------|------------------|---------|-------|
| nuc1  | amd64 | Intel N100  | 4     | 16 GB | talos01     |                  | ceph    |       |
| nuc2  | amd64 | Intel N100  | 4     | 16 GB | talos02     |                  | ceph    |       |
| nuc3  | amd64 | Intel N100  | 4     | 16 GB |             | talos04, talos05 | ceph    |       |
| nixos | amd64 | AMD Ryzen 7 | 16    | 32 GB |             | talos06, talos07 |         | volatile |
| gamer | amd64 | Intel i7    | 28    | 64 GB | talos03     | talos08          |         | volatile |
| rpi1  | ARM   | Cortex-A72  | 4     | 4 GB  |             | talos09          |         |       |
| rpi2  | ARM   | Cortex-A72  | 4     | 4 GB  |             | talos10          |         |       |

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

## Thanks

A big thanks to [onedr0p](https://github.com/onedr0p) for his [template](https://github.com/onedr0p/cluster-template) to bootstrap the cluster. I have been watching his work for years now and it is amazing what he has done for the kubernetes/homelab community. I have [tinkered with](https://github.com/roperscrossroads/kubernetes-flux-gitops) a few iterations of his template over the years and I have learned a lot from doing so, and from looking at other repos based on his work.
