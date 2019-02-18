### Install

```
helm install --name building-blocks-<name> \
    -f building-blocks/values.<name>.yaml \
    --tiller-namespace <namespace> \
    --namespace <namespace> \
    --set global.mongodumpCronJob.enabed=true \
    --set global.mongodumpCronJob.accessKey=access_key \
    --set global.mongodumpCronJob.secretKey=secret_key \
    --set authorization-server.sessionSecret=session_secret \
    --set mongodb.mongodbRootPassword=mongo_password \
    --set mongodb.mongodbPassword=mongo_password \
    building-blocks
```

### Delete

```
helm del --purge building-blocks-<name> --tiller-namespace <namespace>
```

### Upgrade

```
helm upgrade building-blocks-<name> \
    --tiller-namespace <namespace> \
    --namespace <namespace> \
    --reuse-values \
    --recreate-pods \
    --wait \
    helm-charts/building-blocks
```

### Other Resources

To install letsencrypt ssl along with cert-manager. (requires cert-manager and nginx-ingress installed)

```
# Create ClusterIssuer for domain
$ kubectl apply -f cert-manager-ingress/cluster-issuer.yaml

# Create Certificate
$ kubectl apply -f cert-manager-ingress/certificate.yaml
```

Notes:

- PersistentVolumeClaim for 1Gi for storing app data, mongodb data and redis' data
- annotations for ingress certmanager.k8s.io/cluster-issuer: letsencrypt-prod the issuer created above.
- Redis Chart is customised based on simple docker-compose like setup with no cluster
