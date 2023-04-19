# Argo rollouts blue green demo

Argo rollouts demo based on argoproj + codefresh examples.

Expected demo time: 10-15 mins

## Requirements

- Kubernetes cluster ( for example with Docker Desktop )
- Argo rollouts installed to kubernetes cluster: [instructions](https://argoproj.github.io/argo-rollouts/installation/#controller-installation)
- Argo rollouts kubectl plugin installed: [instructions](https://argoproj.github.io/argo-rollouts/installation/#kubectl-plugin-installation)


## Demo

1. Deploying a rollout

Run the following command to deploy the initial rollout + services

`kubectl apply -f .`

Open visualization of the rollout to another terminal window with:

`kubectl argo rollouts get rollout rollouts-demo --watch`

To view the deployed service expose it with

`kubectl port-forward service/rollout-bluegreen-active 8080:80`

+ navigate to localhost:8080 on browser

2. Updating a rollout

Run argo rollouts set image command to update the image.
```
  kubectl argo rollouts set image rollouts-demo \
  rollouts-demo=argoproj/rollouts-demo:yellow
```

To view the preview service, expose it with

`kubectl port-forward service/rollout-bluegreen-preview 8081:80`

3. Promoting a rollout

To promote the rollout:

`kubectl argo rollouts promote rollouts-demo`

After this only the active service should be only one available

Refresh the port forwards to view the current situation, ( ctrl + c, rerun the command)

### Bonus

View the argo-rollouts ui with

`kubectl port-forward service/<my-release>-argo-rollouts-dashboard 31000:3100 -n argo-rollouts`



## References

https://codefresh.io/learn/argo-rollouts/

https://argoproj.github.io/argo-rollouts/getting-started/

https://argoproj.github.io/argo-rollouts/installation/#kubectl-plugin-installation

