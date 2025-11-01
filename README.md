<div align="center">
  <img width="100" height="100" src="https://avatars.githubusercontent.com/u/190339082" >
  <h2>𐬺 TinyO</h2>
  <h5>Just orchestrate.</h5>
  <p align="center">
    <a href="#vision"><b>Why</b></a> •
    <a href="#quickstart"><b>Quickstart</b></a> •
    <a href="https://discord.gg/ERKBk6ArnQ" target="_blank"><b>Discord</b></a> •
    <a href="https://x.com/PureLinux" target="_blank">𝕏</a>
  </p>
</div>

**TIO** - A minimal [Linux®][linux.org] **orchestrator**.

[1/8 components:](#components)
- [tinyoctl-k8s-converter][tinyoctl-k8s-converter]: Converts [K8s][kubernetes.io] `yaml` Statefile to TIO Statefile and `helm` to TIO `apt` ([Vision](#vision)).

Inspired by [Tenstorrent][tenstorrent.com], [K8s][kubernetes.io], [tinygrad][tinygrad.org].

<blockquote>
 <span>
  A GitHub ⭐️ would support the open-source ecosystem of TIO in a meaningful way.
 </span>
</blockquote>

## Benchmark

| Measurements                | TIO   | [K8s][kubernetes.io] | [Podman][containers/podman] |
|-----------------------------|-------|-----|----------------|
| Container Startup Time (alpine:x.y.z) [s] | WIP   | WIP | WIP            |
| Cluster RAM Size [mb]       | **~288**   | **[~5,476][docs-k8s-ram-size]** | -            |
| Cluster Disk Size [mb]      | **~144**   | **[~2,750][docs-k8s-binary-size]** | -            |
| System Binary Size (total) [mb] | **~50**   | **[~2,770][docs-k8s-binary-size]** | WIP            |

<blockquote>
 <span>
    It's tiny, but it's fast.
 </span>
</blockquote>

**System:**
- [Ubuntu Server][ubuntu-server] 24.04.1 LTS
- [OVH VPS Comfort][ovhcloud.com] (4 vCore, 8 GB, 160 GB SSD NVMe, 1 Gbps)

**Last update:** WIP

**TIO:** (HA, 3 Mesh Nodes)

**K8s:** (HA, 3 Master, 2 Worker Nodes)

**Podman:** WIP

---

- [Benchmark](#benchmark)
- [☁️ Overview](#️-overview)
    - [Challenge](#challenge)
- [Features](#features)
  - [Simplicity](#simplicity)
  - [Cluster](#cluster)
  - [Runtime](#runtime)
    - [Optimized Intra-Node Containers](#optimized-intra-node-containers)
      - [⚡️ Direct Network](#️-direct-network)
        - [Key Features](#key-features)
        - [Benefits](#benefits)
      - [➕ Instant Duplication](#-instant-duplication)
        - [Key Features](#key-features-1)
        - [Benefits](#benefits-1)
- [🏁 Quickstart](#-quickstart)
- [Usage](#usage)
- [Architecture](#architecture)
  - [Components](#components)
- [Vision](#vision)
  - [Roadmap](#roadmap)
    - [Phase 1: Bicycle](#phase-1-bicycle)
    - [Phase 2: Car](#phase-2-car)
    - [Dashboard Pro](#dashboard-pro)
      - [Concept](#concept)
- [PureLinux DAO](#purelinux-dao)
  - [Important IP contributors](#important-ip-contributors)
  - [Financial Sponsors](#financial-sponsors)
  - [1337 H4x0r](#1337-h4x0r)
        - [Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries.](#linux-is-the-registered-trademark-of-linus-torvalds-in-the-us-and-other-countries)

---

## ☁️ Overview

This is the **alpha** version of **TIO**.

**Status:** We're working on the first MVP (1 node **localhost** `cluster` for **Linux®** & **MacOS®**).

#### Challenge

<blockquote>
 <span>
    If you can break it, you truly understand it.
 </span>
</blockquote>

If you're able to delete lines and/or break the [runtime (tinyort)][tinyort] in any meaningful way, you will be listed in [1337 H4x0r](#1337-h4x0r). Please be kind, this is an early alpha. [![pure-linux-discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ)

## Features

Some of the features of TIO are inspired from [k8s/complexities.md][repo-docs-vision-comparisons-k8s-complexities.md].

### Simplicity

- **🍦 CLI**: Minimal [cli](#-usage) (e.g. `tio + l.yml`).
- **𐬺 Config:** Minimal [Statefiles](#-usage) (`yml`).
  - Decentralized `cluster` mesh (VPN: [Nebula based][tinyolet-docs-vpn-manager-options-analysis.md], [More Details][tinyolet])
  - Built-in `user` management with intuitive `cli` login
  - Built-in `container` `secrets` injection
  - WIP
- **🏁 Quickstart:** Be ready in seconds.
  - [1 curl](#-quickstart) `cluster` setup
    - TIO [ctl/cli][tinyoctl] (`tio`)
    - TIO `cluster` ([tinyolet][tinyolet], [tinyokv][tinyokv], [tinyort][tinyort])
    - ([Docker Hub][hub.docker.com] image (user-selected))
    - ([VSCode Server][vscode-server] (+ [devcontainers][devcontainers/templates]))

### Cluster

<blockquote>
 <span>
    In a nutshell TIO is just an orchestration of runtimes.
 </span>
</blockquote>

- **Efficiency**: **Lowest** possible resource **requirements**
  - RAM (+ Bandwidth)
  - IOPS
  - Disk
  - ➡️ Significantly **smaller** than [K8s][kubernetes.io] for similar tasks (**less** cloud/operation **costs**)
- **Scaling:** Infinite (Network **mesh**)
- **Speed:** Fast ([Rust][rust-lang.org] & **low-level** libs, achieving lowest **container startup** times, WIP)
- **Decentralized mesh**
  - **No master**/worker topology entities.
- **Upgrades:** Hustle free (**simple** system -> better **LTS compatibility**)
- **Recursive:** Cluster in `cluster` (tint) per default (**backup**/**restore** whole clusters with ease using [tinyoctl][tinyoctl])
- **Dynamicity:** E.g. [etcd.io][etcd.io] for [K8s][kubernetes.io] has [important limitations][repo-docs-vision-comparisons-k8s#etcd-limitations] we want to address with [tinyokv][tinyokv].

### Runtime

#### Optimized Intra-Node Containers

##### ⚡️ Direct Network

| Measurements                | TIO   | [K8s][kubernetes.io] | [Podman][containers/podman] |
|-----------------------------------------------|-------|------|----------------|
| Container to Container Network Throughput [mb]  | WIP   | WIP  | WIP            |

TIO introduces an innovative feature for optimizing container communication on the same node, **reducing overhead** and improving performance. Unlike traditional networking approaches that rely on full TCP/IP stacks or ingress mechanisms, this runtime leverages **direct communication** methods tailored for **Linux** architectures.
Standard mechanisms will be added in the future to keep more advanced features **optional**.

###### Key Features

- **Unix Domain Sockets (`UDS`):** Enables fast and efficient inter-container communication without the overhead of TCP/IP. Each container communicates via `UDS` managed by the runtime.
- **Shared Memory (`shm`):** Facilitates low-latency data exchange by sharing memory regions between containers for intensive data transfers.
- **Kernel Bypass with `eBPF`:** Utilizes `eBPF` for advanced packet routing and filtering, optimizing node-level communication pipelines.
- **Direct Process Piping:** Supports lightweight communication using `POSIX` pipes for simpler `IPC` requirements.

###### Benefits

- **Performance Boost:** Drastically reduces network latency and overhead compared to standard container networking.
- **Secure Isolation:** Maintains strict namespace isolation and access control to ensure container security.
- **Customizability:** Designed for flexible implementation to fit diverse container workloads.

##### ➕ Instant Duplication

| Measurements                | TIO   | [K8s][kubernetes.io] | [Podman][containers/podman] |
|-----------------------------------------------|-------|------|----------------|
| 1000 alpine:x.y.z Container Parallel Start [s]    | WIP   | WIP  | WIP            |

This feature introduces an approach to container instantiation based on existing ones in **milliseconds** on a single node. Instead of traditional container creation workflows, which rely on extracting and initializing container images from scratch, this method enables **low-level duplication of existing containers** already running on the node. This drastically reduces the time required to spin up identical containers, providing a significant performance boost for scenarios requiring rapid scaling or cloning.

###### Key Features

- **Low-Level Duplication:** Leverages Linux® kernel features to clone running containers directly, bypassing traditional workflows for image extraction and initialization, enabling seamless replication.
- **Blazing Fast Startup Times:** Launches new containers in milliseconds by reusing filesystem layers, memory, and resources from existing containers on the same node.
- **Dynamic Resource Optimization:** Detects and reuses running containers on the node, minimizing redundant resource allocation and improving performance.
- **Advanced Filesystem Snapshotting:** Uses cutting-edge Linux® technologies like `overlayfs` and copy-on-write (`CoW`) layers to efficiently duplicate container filesystems without full re-extraction.
- **Secure Namespace Cloning:** Maintains container isolation while replicating Linux® namespaces (`PID`, `IPC`, `UTS`, etc.), ensuring secure and consistent environments for each instance.
- **Memory Optimization with KSM:** Employs Kernel Same-page Merging (`KSM`) to share common memory pages between duplicated containers, reducing memory overhead without sacrificing performance.
- **Rust-Powered Efficiency:** Built with Rust for high-performance, low-level operations, ensuring safe and reliable container duplication with minimal system impact.

###### Benefits

- **Rapid Scaling:** Scale up workloads almost instantly by duplicating existing containers on-demand.
- **Significant Speedup:** Duplication is faster than traditional container creation methods, even those optimized by tools like Kubernetes.

Please give the **community feedback** about your opinion regarding the development of TIO ([Issues][repo-issues]/[Commits][repo-commits]/[Discussions][repo-discussions]).

## 🏁 Quickstart

Just execute & you're ready to orchestrate on any platform (coming soon). This automatically **installs** `tinyoctl` & **initializes** a local **cluster** on the host system. **Be ready in seconds:**

```bash
sh curl tinyo.io/get | bash
```

Deploy a **[VSCode Server][vscode-server]** with a user-selected **[Docker Hub][hub.docker.com]** image in just one click and a magic password using [tinyocloud][tinyocloud] (WIP).

Running TIO **requires root** due to the use of **Linux® namespaces**, pivot_root, mounting filesystems, modifying network interfaces and so on.
Ensure you have the necessary permissions and understand the **security implications** before using TIO Alpha.

⚠️ The current alpha version of TIO should only be used in a controlled environment, such as a **virtual machine** (or container, but currently not supported) to prevent **unintended side effects** on your **host system**.

## Usage

<blockquote>
 <span>
    We try to achieve more with less.
 </span>
</blockquote>

TIO uses **minimal Statefiles** (`yml`) which are managed via [tinyoctl][tinyoctl] cli.

First **setup** the first `cluster` **node** via `tinyoctl` cli (alias **tio**) by providing a network name, username & password of your initial admin user:
```sh
tio ++ -net [network_name] -u [admin_username] -p [admin_password]
```

To **add** more **nodes** just execute the command above on a different host system with the following `tinyoctl` flag in addition:
```sh
-ip [IP of any other existing node]
```

To **isolate containers** just **create** additional **clusters**. A container has **network access** to **any** other container in one cluster.

Here is an **example** to create 1 container with 1 port & 2 mounts:

```sh
tio + alpine-1.yml
```

```yaml
# Source: https://github.com/pure-linux/tinyoctl/blob/release/alpha/0.0.1/examples/basic/alpine-1.yml
container: "alpine:latest"
port: 8080
mounts:
  - source: "/etc/hosts"
    target: "/mnt/hosts"
  - source: "/tmp/local-config"
    target: "/config"
```

## Architecture

### Components

The system has the following **4 main components**. [tinyoctl][tinyoctl] interacts with [tinyolet][tinyolet] to start [tinyort][tinyort]. [tinyokv][tinyokv] is the data store for the TIO `cluster` [node(s)][tinyolet].
Don't worry about master/worker nodes and so on. The system operates similarly to a **mesh** topology:

- **[tinyoctl][tinyoctl]:** Contains cli and packages intended for use by client programs.
- **[tinyolet][tinyolet]:** Controller for each `cluster` node. Think of it as biolerplate code which is orchestrating the [runtime][tinyort](s).
- **[tinyokv][tinyokv]:** A high performance distributed Key-Value store for [tinyolet][tinyolet] (WIP).
- **[tinyort][tinyort]:** Runtime

E.g. the [tinyort/src/utils/core.rs][tinyort-src-utils-core.rs] currently has the size of about **350** code lines. The **MVP** should remain **below 2-3k** lines for single localhost container with storage & networking (+ Docker Hub download, ..).

To improve TIO and to make it completely accessible to the entire developer community, we introduced the following **3 additional components:**

- [tinyoapt][tinyoapt]: Package Tool to simplify the setup of various applications within a cluster.
- [tinyodash][tinyodash]: TIO Pro Dashboard for local development & cloud operations.
- [tinyoctl-k8s-converter][tinyoctl-k8s-converter]: Converts [K8s][kubernetes.io] `yaml` Statefile to TIO Statefile and `helm` to TIO `apt` ([Vision](#-vision)).

**1 security related component:**
- [tinyort-fuzzer][tinyort-fuzzer]: Partial automated Fuzzer for the TIO [runtime][tinyort].

## Vision

<blockquote>
 <span>
    Developers want simple, but highly effective tools that reduce (local) infrastructure complexity.
 </span>
</blockquote>

### Roadmap

#### Phase 1: Bicycle

- Minimal **prototype** that addresses localhost development with containers
- MVP version
  - Base `cli`
  - WIP
- WIP

#### Phase 2: Car

- `w` `clusters` in `x` `clusters` with `y` `nodes` containing `z` `containers`
- WIP

#### Dashboard Pro

##### Concept

<div align="center">
  <img width="400" height="400" src="assets/img/demo/dashboard-1.png" >
</div>

**Visualisation:** Full scale TIO `cluster` with multiple `clusters`, `containers`, `storage`, `ingress`, `pipelines`, `scales`, WIP
Source: [k8svisual/vpk][k8svisual/vpk]

---

## PureLinux DAO

➡️ There is a separate repository for the [DAO][pure-linux-dao].

### Important IP contributors

The people that are listed below made important direct and/or indirect contributions to the vision of TIO. It is very important for us to document any credit regarding our very kind [contributors][repo-contributors] of various kinds and to give them their individual fair stake.

- [GitHub username] [IP Summary]

### Financial Sponsors

We are very grateful for every GitHub/.. Sponsor:

- [GitHub username]

### 1337 H4x0r

Experts who successfully deleted lines and/or meaningfully broke the [runtime][tinyort] include:

- Maybe you? [![pure-linux-discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ)

---

**[PureLinux.org][purelinux.org]** | Delivering to the open-source community what matters most.

###### Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries.

[linux.org]: https://www.linux.org
[repo-contributors]: https://github.com/pure-linux/tinyo/graphs/contributors
[repo-issues]: https://github.com/pure-linux/tinyo/issues
[repo-commits]: https://github.com/pure-linux/tinyo/commits
[repo-discussions]: https://github.com/pure-linux/tinyo/discussions
[repo-docs-vision-comparisons-k8s-complexities.md]: ./docs/vision/comparisons/k8s/complexities.md
[repo-docs-vision-comparisons-k8s#etcd-limitations]: ./docs/vision/comparisons/k8s/complexities.md#etcd-limitations-and-control-plane-complexity
[docs-k8s-binary-size]: ./docs/vision/comparisons/k8s/size/binary.md
[docs-k8s-ram-size]: ./docs/vision/comparisons/k8s/size/ram.md
[pure-linux-discord]: https://discord.gg/ERKBk6ArnQ
[pure-linux-dao]: https://github.com/pure-linux/DAO
[tinyoctl]: https://github.com/pure-linux/tinyoctl
[tinyoctl-k8s-converter]: https://github.com/pure-linux/tinyoctl-k8s-converter
[tinyolet]: https://github.com/pure-linux/tinyolet
[tinyokv]: https://github.com/pure-linux/tinyokv
[tinyort]: https://github.com/pure-linux/tinyort
[tinyort-fuzzer]: https://github.com/pure-linux/tinyort-fuzzer
[tinyoapt]: https://github.com/pure-linux/tinyoapt
[tinyodash]: https://github.com/pure-linux/tinyodash
[tinyocloud]: https://github.com/pure-linux/tinyocloud
[tinyort-src-utils-core.rs]: https://github.com/pure-linux/tinyort/blob/release/alpha/0.0.1/src/utils/core.rs
[purelinux.org]: https://purelinux.org
[rust-lang.org]: https://rust-lang.org
[kubernetes.io]: https://kubernetes.io
[k8svisual/vpk]: https://github.com/k8svisual/vpk
[tenstorrent.com]: https://tenstorrent.com
[tinygrad.org]: https://tinygrad.org
[ubuntu-server]: https://ubuntu.com/server
[ovhcloud.com]: https://www.ovhcloud.com/en/vps
[etcd.io]: https://etcd.io
[containers/podman]: https://github.com/containers/podman
[go.dev]: https://go.dev
[hub.docker.com]: https://hub.docker.com
[vscode-server]: https://code.visualstudio.com/docs/remote/vscode-server
[devcontainers/templates]: https://github.com/devcontainers/templates
[tinyolet-docs-vpn-manager-options-analysis.md]: https://github.com/pure-linux/tinyolet/blob/release/alpha/0.0.1/docs/components/vpn-manager/options-analysis.md
