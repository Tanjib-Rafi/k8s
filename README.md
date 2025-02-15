# 🐳 Kubernetes Overview

Kubernetes is a powerful system for managing containerized applications across multiple hosts. It automates deployment, scaling, and operations of application containers.

## 🍲 Pods
A **Pod** is the smallest deployable unit in Kubernetes. It can contain one or more **tightly coupled containers** that work together to complete a task. Containers within a Pod:

- **Share Networking**: All containers in a Pod share the same IP address and network ports.
- **Share Storage**: Containers in the same Pod can access shared storage volumes.

> **Example**: Use a Pod to run a single application container or a set of containers that need to work closely together.

## 📡 Services
Services in Kubernetes manage networking and allow communication between Pods and other parts of the application, both internal and external.

### Service Types:
- **ClusterIP**: Exposes the service within the Kubernetes cluster.  
  _Best for internal-only communication between services._

- **NodePort**: Exposes the service on a specific port on each Node in the cluster.  
  _Accessible externally via `<NodeIP>:<NodePort>`._

- **LoadBalancer**: Creates an external load balancer and assigns a fixed external IP.  
  _Ideal for distributing traffic across multiple Pods._

- **Ingress**: Manages external access to services, typically HTTP/S, and provides load balancing, SSL termination, and name-based virtual hosting.  
  _Allows you to define rules for routing traffic based on URLs or domain names._

### Port Definitions:
In a Kubernetes `Service` specification, the following ports can be defined:

- **port**: 
  - The port that the Service listens on within the cluster.
  - Used by clients to access the Service.

- **targetPort**: 
  - The port on the Pod that the Service forwards traffic to.
  - This is where the actual application listens for requests.

- **nodePort**: 
  - A specific port that is opened on each Node in the cluster when using `NodePort` service type.
  - It allows external traffic to access the Service via `<NodeIP>:<NodePort>`.
  - It is used for development mostly

- **containerPort**: 
  - The port on which the container itself is listening.
  - This is defined in the Pod specification, often used for documentation purposes.
