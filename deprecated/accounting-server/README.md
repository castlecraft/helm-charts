### Install

```
helm install --name accounting-server-staging \
    --tiller-namespace management-tools \
    --namespace management-tools \
    --set NODE_ENV=staging \
    --set postgresql.postgresqlPassword=SuperSecretString \
    --set image.tag=edge \
    --set ingress.hosts={staging-accounting.castlecraft.in} \
    helm-charts/accounting-server
```

### Delete

```
helm del --tiller-namespace management-tools --purge accounting-server-staging
```
