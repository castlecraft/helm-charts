### Install

```
helm install --name building-blocks \
    --tiller-namespace building-blocks \
    --namespace building-blocks \
    --set sessionSecret=SuperSecretString \
    helm-charts/building-blocks
```

### Delete

```
helm del --purge building-blocks
```

### Upgrade

```
helm upgrade building-blocks \
    --tiller-namespace building-blocks \
    --namespace building-blocks \
    --reuse-values \
    --wait \
    helm-charts/building-blocks

```

### Test Helm Install

```sh
helm install --name building-blocks-testing --namespace testing\
    --tiller-namespace testing \
    --set NODE_ENV=staging \
    --set mongodb.persistence.enabled=false \
    --set mongodb.image.repository=registry.gitlab.com/castlecraft/docker-craft/bitnami-mongodb-config \
    --set mongodb.image.tag=latest \
    --set redis.master.persistence.enabled=false \
    --set rabbitmq.persistence.enabled=false \
    --set authorization-server.image.tag=edge \
    --set authorization-server.ingress.enabled=false \
    --set authorization-server.persistence.enabled=false \
    --set communication-server.image.tag=edge \
    --set communication-server.ingress.enabled=false \
    --set communication-server.persistence.enabled=false \
    --set identity-provider.image.tag=edge \
    --set identity-provider.ingress.enabled=false \
    --set identity-provider.persistence.enabled=false \
    --set infrastructure-console.image.tag=edge \
    --set infrastructure-console.ingress.enabled=false \
    --set infrastructure-console.persistence.enabled=false \
    building-blocks
```

### Initialize DBs for MongoDB Container

```sh
docker run -d --name test_mongo \
  -p 27017:27017 \
  -v ./files/docker-entrypoint-initdb.d:/docker-entrypoint-initdb.d \
  -e MONGODB_USERNAME=admin \
  -e MONGODB_PASSWORD=admin \
  -e MONGODB_ROOT_PASSWORD=admin \
  -e MONGODB_DATABASE=test_authorization-server \
  bitnami/mongodb:latest
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
