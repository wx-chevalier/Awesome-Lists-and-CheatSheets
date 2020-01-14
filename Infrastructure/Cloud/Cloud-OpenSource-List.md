[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wx-chevalier/Awesome-Lists)

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

# Kubernetes

## CLI Tools

- [2019-KinD #Project#](https://github.com/kubernetes-sigs/kind/): kind is a tool for running local Kubernetes clusters using Docker container "nodes". kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

- [krew #Project#](https://github.com/GoogleContainerTools/krew): krew is the package manager for kubectl plugins.

- krew plugins: [kubectl-tree](https://github.com/ahmetb/kubectl-tree)

- [Wayne #Project#](https://github.com/Qihoo360/wayne): Web UI for Kubernetes multi-clusters

- [kubectx #Project#](https://github.com/ahmetb/kubectx): Switch faster between clusters and namespaces in kubectl.

## Application Management

- [2019-kruise #Project#](https://github.com/openkruise/kruise): Automate application workloads management on Kubernetes

- [Kubernetes Helm #Project#](https://github.com/kubernetes/helm): Helm is a tool for managing Kubernetes charts. Charts are packages of pre-configured Kubernetes resources.

- [Draft #Project#](https://github.com/Azure/draft): A tool for developers to create cloud-native applications on Kubernetes.

- [Gatekeeper #Project#](https://github.com/open-policy-agent/gatekeeper): Gatekeeper - Policy Controller for Kubernetes -

## Network

- [OpenEBS #Project#](https://www.openebs.io/): OpenEBS is an open source storage platform that provides persistent and containerized block storage for DevOps and container environments.

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
