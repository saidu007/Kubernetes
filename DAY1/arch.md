# Kubernetes (K8s) Architecture - In Detail

## 🌐 Overview
Kubernetes follows a **master-worker (control plane - node)** architecture. It is used to **automate deployment, scaling, and management of containerized applications**.

---

## 🧠 1. Control Plane (Master Node)

This is the **brain** of the Kubernetes cluster. It makes global decisions about the cluster (e.g., scheduling, scaling, etc.).

### 📌 Components of the Control Plane

#### 1.1 kube-apiserver (Front-end of K8s)
- Acts as a **REST API**.
- All commands from `kubectl` go to this component.
- **Handles all communication** within the cluster.
- Authenticates, validates, and processes API requests.

#### 1.2 etcd (Key-Value Store)
- Stores **all cluster data**.
- Acts like a **database** for Kubernetes.
- Example: pod definitions, config maps, secrets, state, etc.

#### 1.3 kube-scheduler
- Decides **which node** should run a new pod.
- Works based on:
  - Resource requirements (CPU, memory)
  - Policies
  - Affinity/Anti-affinity
  - Taints/Tolerations

#### 1.4 kube-controller-manager
- Runs controllers that regulate the state of the cluster.
- Common controllers:
  - **Node Controller** – monitors node health.
  - **ReplicaSet Controller** – ensures desired number of pods.
  - **Job Controller** – runs batch jobs.
  - **Endpoint Controller** – updates endpoints for services.

#### 1.5 cloud-controller-manager
- Used in **cloud environments** (AWS, GCP, Azure).
- Handles:
  - Node lifecycle
  - Load balancers
  - Volumes (block storage)

---

## ⚙️ 2. Worker Nodes (Minions)

These are the **machines (VMs/servers)** where your **containers (Pods)** actually run.

### 📌 Components of a Worker Node

#### 2.1 kubelet
- Agent that runs on every node.
- **Takes instructions from kube-apiserver**.
- Ensures containers are running in pods as expected.

#### 2.2 kube-proxy
- Handles **networking**.
- **Maintains network rules** on the node.
- Enables **service discovery and load balancing** across pods.

#### 2.3 Container Runtime
- Software responsible for running containers.
- Common ones: Docker, containerd, CRI-O.
- It pulls images, starts/stops containers.

---

## 📦 3. Pods

- The **smallest unit** in Kubernetes.
- Wraps one or more containers.
- Pods share the same network namespace and storage.

---

## 🔄 Flow of Operations in Kubernetes

If you run:

```bash
kubectl apply -f pod.yaml


### What Happens:

1. `kubectl` sends the request to `kube-apiserver`.
2. `kube-apiserver` stores the desired state in `etcd`.
3. `kube-controller-manager` detects the new pod requirement.
4. `kube-scheduler` selects a suitable worker node.
5. `kubelet` on that node pulls the image via the container runtime.
6. Pod starts, and `kube-proxy` helps expose it as needed.

---

![Kubernetes Cluster Architecture](https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg)


---

## 📌 Key Terms

| Term             | Description                               |
|------------------|-------------------------------------------|
| **Pod**          | Group of one or more containers           |
| **Node**         | A machine (VM or physical) in the cluster |
| **Control Plane**| Brains of the cluster                     |
| **kubelet**      | Agent running on each node                |
| **kube-proxy**   | Handles networking and service routing    |
| **etcd**         | Key-value store for config and state      |

---

```

Let me know if you want this in a downloadable `.md` file or if you'd like a **diagram image** version!
