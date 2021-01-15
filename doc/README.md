# Learnings

 During the creation of the clc-flagger-project we encountered numerous error messages, warning and other obstacles. Here you can find a collection of helpfull hints.

## Image Update

When updating an image with the `set image` while being connected to a pod, the port-forwaring of the corresponding pod is terminated. 

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/image_update_pod_dies.png)

## Pending pods

You cannot do a rollout with pendings pods. This error occurs during the deployment steps

SOLUTION: Increase the number of nodes in your kubernetes cluster.

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/pending_pods.png)

## Metrics not found

Acording to flagger Documentation, there are two built in metrics that can be used for monitoring. see https://docs.flagger.app/usage/metrics


![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/metric_not_found.png)

## Hall of fame

![alt text](https://github.com/dorian1000/clc_flagger_project/blob/main/images/hell.png)


