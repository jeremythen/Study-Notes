# Kubernetes (K8s)

Containers orchestrator control multiple containers.

Kubernetes schedule and run containers on clusters of virtual machines.

You can use Kubernetes to run applications in Docker on your infrastructure.

## Terms

* Pods (a group of containers, one single unit of deployment)
* CNCF
* etcd
* kubectl (command line interface)
* Work Node
* Kubelet
* Kube-proxy

## Features

* Multi-Host Container Scheduling
* Scalability and Availability
* Flexibility and Modularization
* Registration
* Service Discovery
* Persistent Storage
* Application Upgrades and Downgrades
* Maintenance
* Logging and Monitoring
* Secrets Management
* Cummunity
  * KubeCon
  * Meetups
  * Slack - https://kubernetes.slack.com

# Notes

* Don't create your own orchestrator.

# Kubernetes Architecture

## Master Node

* The API Server
  * The frontend of the kubernetes
* Scheduler
  * Watches, creates pods
* Controller Manager
  * Node controller, orchestration, replication controller, endpoint controller, service account, etc.

# Controllers

## Types

* ReplicaSet
  * Makes sure a specified number of replicas for pods are running at all times.
* Deployment
  * Declartive updates or ReplicaSets and Pods
* 