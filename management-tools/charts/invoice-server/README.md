### Install

```
helm install --name invoice-server-staging \
    --tiller-namespace management-tools \
    --namespace management-tools \
    --set NODE_ENV=staging \
    --set image.tag=edge \
    --set ingress.hosts={staging-manager.castlecraft.in} \
    helm-charts/invoice-server
```

### Delete

```
helm del --tiller-namespace management-tools --purge invoice-server-staging
```
