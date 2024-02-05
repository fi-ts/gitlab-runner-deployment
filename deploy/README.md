# gitlab-runner

Here is how to bootstrap the runner:

```bash
kubectl create namespace gitlab-runner

kubectl create secret generic gitlab-runner-api-token \
    --namespace gitlab-runner \
    --from-literal="values.yaml=runnerToken: <runner-token>"

flux create source git gitlab-runner-deployment --url=https://github.com/fi-ts/gitlab-runner-deployment --branch=main

flux create kustomization gitlab-runner-deployment \
    --source=GitRepository/gitlab-runner-deployment \
    --path="./deploy" \
    --prune=true \
    --interval=60m \
    --wait=true \
    --health-check-timeout=10m
```
