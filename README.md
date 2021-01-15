# clc_flagger_project

The aim of this project is to analyze the progressive delivery Kubernetes operator Flagger and its components. We will create a documentation of deployment steps using service mesh applications, like Istio and Linkerd, and ingress controller, like Contour and Gloo. 

We will highlight their properties, functionality, pro, cons, and their differences. 

Additionally, we will create a tutorial highlighting their usage. 

# Setup

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

The install command automatically creates a namespace  `istio-system`.

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

#### Install Grafana in the `istio-system` namespace

```source
    helm upgrade -i flagger-grafana flagger/grafana \
        --namespace=istio-system \
        --set url=http://prometheus.istio-system:9090 \
        --set user=admin \
        --set password=change-me
```

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/deployments_after_setup.png)

# Deploy Demo App and Canary Resources

Create `test` namespace

```source
    kubectl create ns test
```

Enable Istio sidecar injection

```source
    kubectl label namespace test istio-injection=enabled
```

## Apply Resource files

```source
    kubectl apply -f deployment.yaml -n test

    kubectl apply -f hpa.yaml -n test
```

## Load Tester

Service to generate request during canary analysis
```source
    kubectl apply -k https://github.com/fluxcd/flagger//kustomize/tester?ref=main
```

## Apply Custom Canary Resource

```source
    kubectl apply -f canary.yaml -n test
```

### Verify deployments & pods

```source
    kubectl get deployments -n test
```

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/deployments_ns_test.png)

Check for running pods, if one or more pods are on status pendin see #refLearnings.

```source
    kubectl get pods -n test
```

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/pods_ns_test.png)

### Verify Initialization

```souce
    kubectl -n test describe canary/initdeployment
```

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/describe_canary_resource.png)

# Canary Deployment

To execute a canary deployment, set a new image on your desired resource. This will trigger a canary deployment. Later we´ll see how to read the relevant messages.

```source
    kubectl -n test set image deployment/initdeployment initdeployment=dorian1000/flagger-demo-app:0.0.2
```






