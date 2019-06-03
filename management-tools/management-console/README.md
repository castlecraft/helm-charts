### Install

```
helm install --name management-console-staging \
    --tiller-namespace management-tools \
    --namespace management-tools \
    --set NODE_ENV=staging \
    --set image.tag=edge \
    --set ingress.hosts={staging-manager.castlecraft.in} \
    helm-charts/management-console
```

### Delete

```
helm del --tiller-namespace management-tools --purge management-console-staging
```
