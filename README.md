# kubernetes


<b>A master node runs the following control plane components:</b>

API Server

Scheduler

Controller Managers

Data Store.

In addition, the master node runs:


Container Runtime

Node Agent

Proxy.


<b>A worker node has the following components:</b>

Container Runtime

Node Agent - kubelet

Proxy - kube-proxy

Addons for DNS, Dashboard user interface, cluster-level monitoring and logging.

<b>Компоненты рабочего узла: среда выполнения контейнера</b>

Docker - although a container platform which uses containerd as a container runtime, it is the most popular container runtime used with Kubernetes

CRI-O - a lightweight container runtime for Kubernetes, it also supports Docker image registries http://cri-o.io/

containerd - a simple and portable container runtime providing robustness

frakti - a hypervisor-based container runtime for Kubernetes https://github.com/kubernetes/frakti#frakti

<b>Компоненты рабочего узла: агент узла - kubelet</b>

The kubelet connects to container runtimes though a plugin based interface - the Container Runtime Interface (CRI). The CRI consists of protocol buffers, gRPC API, libraries, and additional specifications and tools that are currently under development. In order to connect to interchangeable container runtimes, kubelet uses a shim application which provides a clear abstraction layer between kubelet and the container runtime. 


<b>Связь между модулями между узлами</b>

https://github.com/containernetworking/cni

https://github.com/containernetworking/cni#3rd-party-plugins

https://github.com/containernetworking/plugins#plugins

https://github.com/coreos/flannel/

https://www.weave.works/oss/net/

https://www.projectcalico.org/

https://kubernetes.io/docs/concepts/cluster-administration/networking/

Minikube - single-node local Kubernetes cluster, recommended for a learning environment deployed on a single host. https://minikube.sigs.k8s.io/docs/

Kind - multi-node Kubernetes cluster deployed in Docker containers acting as Kubernetes nodes, recommended for a learning environment. https://kind.sigs.k8s.io/docs/

Docker Desktop - including a local Kubernetes cluster for Docker users. https://www.docker.com/products/docker-desktop

MicroK8s - local and cloud Kubernetes cluster, from Canonical. https://microk8s.io/

K3S - lightweight Kubernetes cluster for local, cloud, edge, IoT deployments, from Rancher. https://k3s.io/

<B>Локальная установка</B>

Kubernetes can be installed on-premise on VMs and bare metal.

On-Premise VMs

Kubernetes can be installed on VMs created via Vagrant, VMware vSphere, KVM, or another Configuration Management (CM) tool in conjunction with a hypervisor software. There are different tools available to automate the installation, such as Ansible https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/ or kubeadm. https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/

On-Premise Bare Metal

Kubernetes can be installed on on-premise bare metal, on top of different operating systems, like RHEL, CoreOS, CentOS, Fedora, Ubuntu, etc. Most of the tools used to install Kubernetes on VMs can be used with bare metal installations as well. 


kubeadm 

kubeadm is a first-class citizen on the Kubernetes ecosystem. It is a secure and recommended method to bootstrap a multi-node production ready Highly Available Kubernetes cluster, on-prem or in the cloud. Kubeadm can also bootstrap a single-node cluster for learning. It has a set of building blocks to setup the cluster, but it is easily extendable to add more features. Please note that kubeadm does not support the provisioning of hosts. 

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/


kubespray

With kubespray (formerly known as kargo), we can install Highly Available production ready Kubernetes clusters on AWS, GCE, Azure, OpenStack, vSphere, or bare metal. Kubespray is based on Ansible, and is available on most Linux distributions. It is a Kubernetes Incubator project. 

https://kubernetes.io/docs/setup/production-environment/tools/kubespray/

https://github.com/kubernetes-sigs/kubespray


kops

With kops, we can create, upgrade, and maintain production-grade, Highly Available Kubernetes clusters from the command line. It can provision the machines as well. Currently, AWS is officially supported. Support for GCE and OpenStack is in beta, VMware vSphere is in alpha support, and other platforms are planned for the future. Explore the kops project for more details. 


https://kubernetes.io/docs/setup/production-environment/tools/kops/

https://github.com/kubernetes/kops

kube-aws

With kube-aws we can create, upgrade and destroy Kubernetes clusters on AWS from the command line. Kube-aws is also a Kubernetes Incubator project. 

https://github.com/kubernetes-incubator/kube-aws


<b>Требования для запуска Minikube</b>

Minikube use https://github.com/docker/machine/tree/master/libmachine

kubeadm

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/

Below we outline the requirements to run Minikube on our local workstation: 

VT-x/AMD-v virtualization must be enabled on the local workstation in BIOS, and/or verify if virtualization is supported by your workstation's OS.

kubectl

https://kubernetes.io/docs/tasks/tools/install-kubectl/

kubectl is a binary used to access and manage any Kubernetes cluster. It is installed through Minikube and accessed through the minikube command, or it can be installed separately. We will explore kubectl in more detail in future chapters.
Type-2 Hypervisor or Container Runtime
On Linux VirtualBox, https://www.virtualbox.org/wiki/Downloads

KVM2 https://www.linux-kvm.org/page/Main_Page

or Docker and Podman runtimes

On macOS VirtualBox, https://www.virtualbox.org/wiki/Downloads

HyperKit, https://github.com/moby/hyperkit

VMware Fusion, http://www.vmware.com/products/fusion.html

Parallels https://minikube.sigs.k8s.io/docs/drivers/parallels/  or Docker runtime

On Windows VirtualBox, Hyper-V, or Docker runtime.

Minikube supports a --driver=none (on Linux) option that runs the Kubernetes components directly on the host OS and not inside a VM. With this option a Docker installation is required and a Linux OS on the local workstation, but no hypervisor installation. If you use --driver=none in Debian or its derivatives, be sure to download .deb Docker packages instead of the snap package which does not work with Minikube. In addition to hypervisors, Minikube also supports a limited number of container runtimes, with the --driver=docker (on Linux, macOS, and Windows) and --driver=podman (on Linux) options, to install and run the Kubernetes cluster on top of a container runtime. 

https://minikube.sigs.k8s.io/docs/

https://kubernetes.io/docs/setup/learning-environment/minikube/

https://github.com/kubernetes/minikube

<b>Установка Minikube в Linux, Ubuntu Linux 18.04 LTS with VirtualBox v6.1</b>

https://kubernetes.io/docs/tasks/tools/install-minikube/

Verify the virtualization support on your Linux OS (a non-empty output indicates supported virtualization):


$ grep -E --color 'vmx|svm' /proc/cpuinfo

Install the VirtualBox hypervisor
Add the source repository for the bionic distribution (Ubuntu 18.04), download and register the public key, update and install:

$ sudo bash -c 'echo "deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian bionic contrib" >> /etc/apt/sources.list'

$ wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -

$ sudo apt update

$ sudo apt install -y virtualbox-6.1

Install Minikube

We can download the latest release or a specific release from the Minikube release page. Once downloaded, we need to make it executable and add it to our PATH:

$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/


Start Minikube

We can start Minikube with the minikube start command, that bootstraps a single-node cluster with the latest stable Kubernetes version release. For a specific Kubernetes version the --kubernetes-version option can be used as such minikube start --kubernetes-version v1.19.0 (where latest is default and acceptable version value, and stable is also acceptable):

$ minikube start


