# clc_flagger_project

The aim of this project is to analyze the progressive delivery Kubernetes operator Flagger and its components. We will create a documentation of deployment steps using service mesh applications, like Istio and Linkerd, and ingress controller, like Contour and Gloo. 

We will highlight their properties, functionality, pro, cons, and their differences. 

Additionally, we will create a tutorial highlighting their usage. 

## Setup

### Cluster erstellen

Kubernetes Cluster lt. Anleitung in exercise 3.1 erstellen

### Download Istio

https://github.com/istio/istio/releases/tag/1.8.1

### Download helm

https://github.com/helm/helm/releases

Add a repository to helm. Flagger is later installed using this helm repository.

```
    helm repo add flagger https://flagger.app
```

### Install required Services to Kubernetes Cluster

#### Install Istio

```source
    istioctl install --set profile=default
```

#### Install Prometheus
```source
    kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.8/samples/addons/prometheus.yaml
```

#### Install Flagger for Istio in the `istio-system` namespace
```source
    kubectl apply -k github.com/fluxcd/flagger//kustomize/istio
```

#### 

```source
    kubectl get deployment -n istio-system
```

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/deployments_after_setup.png)

# Demo

