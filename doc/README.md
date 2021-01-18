# Learnings

 During the creation of the clc-flagger-project we encountered numerous error messages, warning and other obstacles. Here you can find a collection of helpfull hints.

## Image Update

When updating an image with the `set image` while being connected to a pod, the port-forwaring of the corresponding pod is terminated. 

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/image_update_pod_dies.png)

## Pending pods

You cannot do a rollout with pendings pods. This error occurs during the deployment steps

**SOLUTION**: Increase the number of nodes in your kubernetes cluster.

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/pending_pods.png)

## Metrics not found

According to flagger Documentation, there are two built in metrics that can be used for monitoring. see https://docs.flagger.app/usage/metrics

* request-success-rate: Uncomment the metric for a successfull rollout. see [Canary.yaml](https://github.com/dorian1000/clc_flagger_project/blob/main/resource/canary.yaml)
* request-duration: Warnings occur in the event log but the promotion completes successfully.

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/metric_not_found.png)

## Hall of fame

We got the error when starting a stopped kubernetes cluster in our azure resource group

```
az aks start --name myAKSCluster --resource-group myResourceGroup
```

If you see this red block of code do not panic. We waited for couples of minutes and executed the command again.

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/hell.png)


