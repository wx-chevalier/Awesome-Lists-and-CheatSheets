# Cloud OpenSource List

# Virtualization

- [LightVM #Project#](http://cnp.neclab.eu/projects/lightvm/): . With LightVM we examine whether there is indeed a strict tradeoff between isolation (VMs) and efficiency (containers). We find that VMs can be as nimble as containers, as long as they are small and the toolstack is fast enough.

- [TinyVM #Project#](https://github.com/jakogut/tinyvm): TinyVM is a virtual machine with the goal of having a small footprint. Low memory usage, a small amount of code, and a small binary.

- [gVisor #Project#](https://github.com/google/gvisor): gVisor is a user-space kernel, written in Go, that implements a substantial portion of the Linux system surface.

- [Kata Containers #Project#](https://katacontainers.io/): Kata Containers is a new open source project building extremely lightweight virtual machines that seamlessly plug into the containers ecosystem.

- [Hyper Container #Project#](https://hypercontainer.io/): Hypervisor-agnostic Docker Runtime.

# Docker

## Tool

- [ctop #Project#](https://github.com/bcicen/ctop): Top-like interface for container metrics

- [container-diff #Project#](https://github.com/GoogleCloudPlatform/container-diff): container-diff is a tool for analyzing and comparing container images. container-diff can examine images along several different criteria

- [dive #Project#](https://github.com/wagoodman/dive): A tool for exploring each layer in a docker image.

- [2019-docker-slim #Project#](https://github.com/docker-slim/docker-slim): DockerSlim (docker-slim): Don't change anything in your Docker container image and minify it by up to 30x (and for compiled languages even more) making it secure too! (free and open source)

## Storage | 存储

- [2015-Flocker #Project#](https://github.com/ClusterHQ/flocker): Flocker is an open-source Container Data Volume Manager for your Dockerized applications.

- [2017-REX-Ray #Project#](https://github.com/thecodeteam/rexray): REX-Ray is a container storage orchestration engine enabling persistence for cloud native workloads

- [GlusterFS #Project#](https://github.com/gluster/glusterfs): Gluster is a software defined distributed storage that can scale to several petabytes. It provides interfaces for object, block and file storage.

## Registry

- [Dragonfly #Project#](https://github.com/alibaba/Dragonfly): Dragonfly is an intelligent P2P based file distribution system. It aims to resolve issues related to low-efficiency, low-success rate and waste of network bandwidth in file transferring process.

- [Harbor #Project#](https://goharbor.io/): Harbor is an open source container image registry that secures images with role-based access control, scans images for vulnerabilities, and signs images as trusted.

- [registry-cli #Project#](https://github.com/andrey-pohilko/registry-cli): Scripts for easy manipulation of docker-registry from command line (and from scripts).

# Kubernetes

## Tools & Platform

- [krew #Project#](https://github.com/GoogleContainerTools/krew): krew is the package manager for kubectl plugins. krew plugins: [kubectl-tree](https://github.com/ahmetb/kubectl-tree)

- [Wayne #Project#](https://github.com/Qihoo360/wayne): Web UI for Kubernetes multi-clusters

- [kubectx #Project#](https://github.com/ahmetb/kubectx): Switch faster between clusters and namespaces in kubectl.

- [Rancher #Project#](https://github.com/rancher/rancher): Rancher is an open source project that provides a container management platform built for organizations that deploy containers in production. Rancher makes it easy to run Kubernetes everywhere, meet IT requirements, and empower DevOps teams.

- [Lens #Project#](https://github.com/lensapp/lens): Lens is the only IDE you’ll ever need to take control of your Kubernetes clusters. It is a standalone application for MacOS, Windows and Linux operating systems. It is open source and free.

## Distribution

- [2019-k3s #Project#](https://github.com/rancher/k3s): Lightweight Kubernetes. Easy to install, half the memory, all in a binary less than 40mb.

- [2019-KinD #Project#](https://github.com/kubernetes-sigs/kind/): kind is a tool for running local Kubernetes clusters using Docker container "nodes". kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

- [2020-Microk8s #Project#](https://microk8s.io/#get-started): Super-simple production-grade upstream K8s. One-command install on 42 flavours of Linux. Made for developers and devops. Great for edge and IoT.

- [2020-k3d #Project#](https://github.com/rancher/k3d/): Little helper to run Rancher Lab's k3s in Docker.

- [2020-k0s #Project#](https://github.com/k0sproject/k0s): k0s is yet another Kubernetes distro. Yes. But we do some of the things pretty different from other distros out there.

## Cluster Management

- [fleet #Project#](https://github.com/rancher/fleet): Manage large fleets of Kubernetes clusters.

- [oneinfra #Project#](https://github.com/oneinfra/oneinfra): oneinfra is a Kubernetes as a Service platform. It empowers you to provide or consume Kubernetes clusters at scale, on any platform or service provider. You decide.

- [k9s #Project#](https://k9scli.io/): K9s is a terminal based UI to interact with your Kubernetes clusters. The aim of this project is to make it easier to navigate, observe and manage your deployed applications in the wild. K9s continually watches Kubernetes for changes and offers subsequent commands to interact with your observed resources.

## Application Management

- [2019-kruise #Project#](https://github.com/openkruise/kruise): Automate application workloads management on Kubernetes

- [Helm #Project#](https://github.com/kubernetes/helm): Helm is a tool for managing Kubernetes charts. Charts are packages of pre-configured Kubernetes resources.

- [Draft #Project#](https://github.com/Azure/draft): A tool for developers to create cloud-native applications on Kubernetes.

- [Gatekeeper #Project#](https://github.com/open-policy-agent/gatekeeper): Gatekeeper - Policy Controller for Kubernetes -

- [Kubernetes API Gateway #Project#](https://www.getambassador.io/products/edge-stack/api-gateway/): The Ambassador API Gateway delivers the scalability, security, and simplicity for some of the world's largest Kubernetes installations.

- [KubeEdge #Project#](https://github.com/kubeedge/kubeedge): KubeEdge is built upon Kubernetes and extends native containerized application orchestration and device management to hosts at the Edge.

## Network

- [OpenEBS #Project#](https://www.openebs.io/): OpenEBS is an open source storage platform that provides persistent and containerized block storage for DevOps and container environments.

- [Cilium #Project#](https://github.com/cilium/cilium): Cilium is open source software for providing and transparently securing network connectivity and loadbalancing between application workloads such as application containers or processes.

## Storage

- [Rook #Project#](https://github.com/rook/rook): Rook is an open source cloud-native storage orchestrator for Kubernetes, providing the platform, framework, and support for a diverse set of storage solutions to natively integrate with cloud-native environments.

- [Velero #Project#](https://github.com/vmware-tanzu/velero): Velero (formerly Heptio Ark) gives you tools to back up and restore your Kubernetes cluster resources and persistent volumes. You can run Velero with a cloud provider or on-premises.

- [Stash #Project#](https://github.com/stashed/stash): Stash by AppsCode is a Kubernetes operator for restic. If you are running production workloads in Kubernetes, you might want to take backup of your disks.

## CI & CD

- [2018-Kubernetes Client #Project#](https://github.com/kubernetes-client): This organization hosts Kubernetes API client libraries.

- [Skaffold #Project#](https://github.com/GoogleCloudPlatform/skaffold): Skaffold is a command line tool that facilitates continuous development for Kubernetes applications.

- [Brigade #Project#](https://github.com/Azure/brigade): Script simple and complex workflows using JavaScript. Chain together containers, running them in parallel or serially. Fire scripts based on times, GitHub events, Docker pushes, or any other trigger. Brigade is the tool for creating pipelines for Kubernetes.

## HA

- [kube-prometheus #Project#](https://github.com/coreos/kube-prometheus): Use Prometheus to monitor Kubernetes and applications running on Kubernetes.

# Orchestration
