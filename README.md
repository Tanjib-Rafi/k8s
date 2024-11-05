# 🐳 Kubernetes Overview

Kubernetes is like a restaurant kitchen management system, organizing and handling tasks (Pods) to ensure each request is efficiently processed and served.

## 🍲 Pods
A **Pod** is the smallest deployable unit in Kubernetes. It can contain one or more **tightly coupled containers** that work together. Containers within a Pod:

- **Share networking** (same IP address and ports)
- **Share storage** (access to shared volumes)

> **Example:** Think of a Pod as a group of chefs working together to make a dish, sharing the same tools and ingredients.

## 📡 Services
Services in Kubernetes set up networking to allow communication between Pods and manage how users or other services access them.

### Service Types:
- **ClusterIP**: Exposes the service within the Kubernetes cluster.  
  _Best for internal-only traffic between services._
  
- **NodePort**: Exposes the service on a specific port on each Node in the cluster.  
  _Accessible from outside the cluster via `<NodeIP>:<NodePort>`._

- **LoadBalancer**: Creates an external load balancer (on supported cloud providers) and assigns a fixed, external IP.  
  _Great for distributing traffic across multiple Pods._

- **Ingress**: Manages external access to services, usually via HTTP/S.  
  _Allows you to define rules for routing traffic based on URLs or domain names._
