# clc_flagger_project

The aim of this project is to analyze the progressive delivery Kubernetes operator Flagger and its components. We will create a documentation of deployment steps using service mesh applications, like Istio and Linkerd, and ingress controller, like Contour and Gloo. 

We will highlight their properties, functionality, pro, cons, and their differences. 

Additionally, we will create a tutorial highlighting their usage. 

# Setup

## Cluster erstellen

Kubernetes Cluster lt. Anleitung in exercise 3.1 erstellen

## Download Istio

## Download helm

## Install Flagger & Grafana

https://docs.flagger.app/install/flagger-install-on-kubernetes

## Install Istio

https://docs.flagger.app/tutorials/istio-progressive-delivery

## Prerequisites

```source
    istioctl manifest install --set profile=default
```
```source
    kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.8/samples/addons/prometheus.yaml
```
```source
    kubectl apply -k github.com/fluxcd/flagger//kustomize/istio -n istio-system
```
```source
    kubectl get deployment -n istio-system
```

# Demo
