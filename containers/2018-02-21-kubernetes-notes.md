# Kubernetes Notes
> :calendar: *February 21, 2018*

These are my notes from research on Kubernetes.

Before getting started with Kubernetes:
  - Know how the internet works
  - Be very comfortable with Linux and the command line
    * Don't assume you'll do everything in a web-based GUI like Tectonic, Rancher, or the Kubernetes Dashboard
  - Be familiar with the host layers of the OSI model (specifically L4 and L7)
    * This comes in handy when working with different load balancers
  - Have fundamental Docker experience:
    * Containerizing applications (Dockerfiles and `docker build`)
    * Exposing and publishing ports
    * Bridge and Host networks
    * DNS lookup for user-defined networks
    * Named volumes and mount types (volume vs bind)
    * Container registries (i.e., Docker Hub)
    * Running application stacks with Docker Compose
  - Have basic Docker Swarm experience:
    * Manager/worker architecture
    * Swarm management with Docker Machine
    * Replicating and scaling containers
    * The overlay network driver
    * Network ingress
  - Be familiar with microservices architecture
    - Kubernetes has built-in service registration and discovery, but you should know what that means
  - Be familiar with stateless authentication (i.e., JSON Web Tokens)
    * Not directly applicable to Docker/Kubernetes, but you want your containers to be stateless whenever possible
  - Have experience with YAML and/or JSON files

## Getting Started

The easiest (and in my opinion best) way to use Kubernetes is using Google Kubernetes Engine. GKE
manages the Master and ETCD cluster for you (at no additional cost). You simply pick the number
of Nodes you want in your cluster, their compute/memory/storage capacity and what operating system
to run on them. The recommendation is a 3-node cluster running CoreOS.

GKE also has (in my opinion) the best integration with a cloud load balancer and Kubernetes Ingress,
but it will cost extra. Overall expect to pay $60/mo total, but you'll have a rock-solid cluster
with L7 load balancing and self-updating and self-healing Nodes. Google will guarantee uptime of the
Master and ETCD cluster. You'll also get free log management with StackDriver (monitoring costs
extra).

You can also roll your own cluster on DigitalOcean and even use a Kubernetes management tool like
Rancher, but I found the price to be similar to GKE. You could run a $15 cluster (Master + 2 Nodes),
but you won't have much capacity left for your applications and databases since just running
Kubernetes does use quite a bit of system resources.

Overall, I think the general consensus is that cloud-provider managed Kubernetes is the way to go.
For production scenarios, you need to factor how much time you want to allocate to managing
Kubernetes and how much time you want to spend actually developing applications. Keep in mind that
Kubernetes is an enterprise solution (it powers Google) and for running a blog and some personal web
apps, it's probably overkill (but it's such cool tech that you'll probably want to use it anyways).

For local development and just getting comfortable with Kubernetes commands, Minikube is a good way
to get started. Alternatively, the Docker for Windows/Mac programs can deploy a single-node
Kubernetes cluster if you're using the Edge release (as of January 2018).

Kubeadm can be used to create a cluster using your own local or cloud VMs, but it is a little
involved and requires you to set up your own Pod network (WeaveNet seems to be the most popular
choice).

Finally, if you're using Ubuntu, you can run `conjure-up` to deploy a small 2-node cluster, or a
production-ready 3-node cluster running across 9 VMs with EasyRSA, Flannel, 3 dedicated ETCD nodes,
and an Nginx load balancer (you need a very beefy computer to do this). `conjure-up` can take 30-60
minutes to provision and I've also run into issue with ETCD not surviving system reboots, and the
Flannel CIDR needing manual configuration, so Minikube seems to be the best way to go.

## Master Components

Master Components make up the cluster's Control Plane. The Control Plane is responsible for making
the cluster's current state match the desired state - like scaling the number of replicas.

https://kubernetes.io/docs/concepts/overview/components/#master-components

### `kube-apiserver`

Exposes the Kubernetes API, used by `kubectl` and the Kubernetes Dashboard. Can also be interacted
with using Client Libraries (there are officially-supported client libraries available for Go,
Python, Java, and .NET).

### `etcd`

Highly-available distributed key-value store used for all cluster data.

https://coreos.com/etcd/

### `kube-scheduler`

Watches for newly created pods and assigns a Worker node for them to run on.

### `kube-controller-manager`

Manages controllers. Controllers watch the state of the cluster and make changes to bring the
current state to the desired state.

Controllers include:
  - Node: Responds when nodes go down
  - Replication: Responsible for maintaining the correct number of pods
  - Endpoint: Populates the endpoints object (joins Services and Pods)
  - Service Account/Token: Creates accounts and API access tokens for new namespaces

## Node Components

### `kubelet`

An agent that runs on each node in the cluster. Ensures that containers running in a pod are
healthy. Note that `kubelet` doesn't manage any containers not created by Kubernetes.

### `kube-proxy`

Performs connection forwarding to enable the Kubernetes Service abstraction.

## Kubernetes Objects

Objects are persistent entities that represent the state of the cluster. Objects can describe what
containers are running, the nodes they are running on, and how they behave.

Kubernetes Objects are "records of intent". Once an Object is created, Kubernetes works to ensure
that the Object exists. Creating an Object describes the cluster's desired state.

See [Describing a Kubernetes Object](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/#describing-a-kubernetes-object)
for more.

### Pods

A pod is the basic building block of Kubernetes. It represents a single unit of deployment. Pods can
be made up of one or more containers.

A container running in the same pod as another container is a "sidecar".

Pods are not typically deployed directly - they are managed by a Controller like Deployment,
StatefulSet, or DaemonSet.

See [Pod Overview](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/) for more.

### ReplicaSets and ReplicationControllers

A ReplicationController ensures that a specified number of pod replicas are running at a given time.

A ReplicaSet is the next generation ReplicationController. 

You'll most likely not use ReplicaSets directly, as Deployments create and manage their own
ReplicaSets.

### Deployments

A Deployment Object describes the desired state for the Deployment Controller. The Deployment
Controller will update the current state to the desired state at a controlled rate.

### StatefulSets

While Deployments are intended to be stateless, some applications (like databases) require some
state to persist between Pod lifecycles. StatefulSets allow for the creation, updating, and scaling
of stateful applications.

### DaemonSet

DaemonSets ensure that all Nodes run a copy of a Pod. As Nodes are added to the cluster, Pods are
added to them. As Nodes are removed, Pods are garbage collected. DaemonSets are useful for running
storage daemons, as well as logging/monitoring applications.

### Jobs

A Job creates one or more Pods and ensures that a specified number of them successfully terminate.
If a Pod fails, a new one will be restarted. Jobs can run a single Pod, or multiple Pods in
parallel.

### CronJobs

CronJobs run Jobs at specified times and intervals. A CronJob could be scheduled to run only once at
some time in the future, or repeated indefinitely.

### Services

Pod IP addresses can change as the Pod is destroyed and created. Services provide a policy to
access a specific group of Pods.

### Ingresses

Ingress is an API object that provides access to the Services in a cluster, typically over HTTP.
Ingress can provide load balancing, SSL termination, and name-based virtual hosting.

### Volumes and Persistent Volumes

Containers are ephemeral - when they are restarted, any files written in the container will be lost.

Sometimes containers running in a Pod will need to share files amongst one another.

A Persistent Volume is a resource in the cluster just like a node. PVs have a lifecycle independent
of any Pod that uses the PV.

A Persistent Volume Claim is a request for storage by the user. It is similar to a Pod in the sense
that a Pod consumes Node resources, and a PVC consumes PV resources.

### Secrets

Secrets store passwords and API keys and can be mounted to a volume in a container.

Secrets can be created from a text file, or a base64 encoded string.

### ConfigMaps

ConfigMaps allow you to create configuration objects from `.properties` files. ConfigMap values can
be passed to a Pod as environmental variables.

### Names and UIDs

Names are user-provided strings to identify a Kubernetes resource. Only one object can have a given
name at a time.

UIDs are unique IDs generated by Kubernetes. 

### Namespaces

Think of Namespaces as "virtual" clusters within the same physical cluster.

Namespaces allow the cluster resources to be divided up, which is useful when working on multiple
projects within the same cluster.

> Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a few to tens of users, you should not need to create or think about namespaces at all. - [Kubernetes.io](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces)

### Labels and Selectors

Labels are key-value pairs attached to Objects. Labels are intended to provide identifying
information about Objects and organize collections of Objects.

Selectors allow you to group Objects using equality-based or set-based operators. For example,
Selectors are used to constrain Pods to run on specific Nodes. The `nodeSelector` field is the most
common way to do this. This is known as _node affinity_.

Equality-based operators are `=`, `==`, and `!=`. `=` and `==` are synonyms (unlike `==` and `===`
in JavaScript).

Set-based operators are `in`, `notin`, and `exists`.

### Annotations

In contrast to Labels, Annotations are NOT used to identify and select Objects. Annotations allow
you to attach metadata to an Object, like a timestamp, for example.

### Taints and Tolerations

Taints are applied to Nodes in order to reject Pods that do not tolerate the taints. Unlike labels
which can be used to _attract_ Pods, Taints are used to _repel_ Pods.

In order to schedule a Pod onto a Node with a Taint, the Pod must have a Toleration specified that
either matches the Taint (`Equal`) or simply acknowledges that the Taint exists (`Exists`).

For example, by default, the Kubernetes Master has a `NoSchedule` Taint. In order to schedule a Pod
onto the Master, the Pod would either have to tolerate the Taint, or the Taint would have to be
removed.

```bash
# Remove the taint from the Master
λ kubectl taint nodes --all node-role.kubernetes.io/master-
```

## `kubectl`

`kubectl` is the command-line interface (CLI) for running commands against a Kubernetes cluster.

`kubectl` uses a "kubeconfig" file which contains information about your cluster and other necessary
information to communicate with the cluster. It should be noted that there is no file named
`kubeconfig` - the actual file is located at `~/.kube/config`. You can also run
`kubectl config view` to print the contents of the file.

If you haven't set up `kubectl` yet, the config file can be found at `/etc/kubernetes/admin.conf` in
the Kubernetes Master node.

If you're using Google Kubernetes Engine, you can fetch the kubeconfig by running
`gcloud container clusters get-credentials <YOUR_CLUSTER_NAME>`

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

### Object Management

`kubectl` supports different approaches to creating and managing Kubernetes Objects.

The first approach is to use _Imperative Commands_ - running terminal commands and passing flags.
This approach should only be used in non-production environments. In a real environment, you'll want
to use configuration files tracked in a Git repository.

Imperative Commands are good for practice and when graduating from Docker to Kubernetes.

```bash
λ kubectl run nginx --image nginx
```

The second approach is to use _Imperative Object Configuration_. This approach combines operational
commands (e.g., create), optional flags, and a configuration file.

```bash
λ kubectl create -f deployment-nginx.yaml
```

The final and most advanced approach is to use _Declarative Object Configuration_. Using this
approach, Kubernetes will determine what operation to use. This is useful for entire folders of
configuration files, where each file might require a different operation.

This is my preferred method as the configuration files describe the desired state of the cluster.
Any changes to these files (and subsequent `kubectl apply` command) will cause Kubernetes to
initiate the necessary procedures to bring the current state to the desired state.

This reminds me of how React reconciles changes to the virtual DOM by updating the browser DOM.

```bash
λ kubectl apply -f configs/
```
