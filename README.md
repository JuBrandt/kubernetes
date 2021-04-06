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













