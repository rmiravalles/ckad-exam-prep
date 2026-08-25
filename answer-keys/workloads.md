# 🔑 Workload Answer Keys

## ✅ W-01: Deployment with container port

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: nginx
        image: nginx:1.27
        ports:
        - containerPort: 8080
```

Validate with `kubectl rollout status deployment/web` and `kubectl get pods -l app=web`.

Note: Declaring `containerPort` does not change nginx's listening port; the drill checks manifest fluency. A traffic drill should use an image configured to listen on `8080`, or a Service that targets the actual port.

## ✅ W-02: Rolling update and rollback

```sh
kubectl create deployment api --image=nginx:1.26 --replicas=2
kubectl rollout status deployment/api
kubectl set image deployment/api nginx=nginx:1.27
kubectl rollout status deployment/api
kubectl rollout undo deployment/api
kubectl rollout status deployment/api
```

Validate with `kubectl get deployment api -o jsonpath='{.spec.template.spec.containers[0].image}'`, which must return `nginx:1.26`.

## ✅ W-03: Kustomize overlay

Create this layout:

```text
catalog/
  base/
    deployment.yaml
    kustomization.yaml
  overlays/staging/
    kustomization.yaml
```

`base/deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: catalog
spec:
  replicas: 1
  selector:
    matchLabels:
      app: catalog
  template:
    metadata:
      labels:
        app: catalog
    spec:
      containers:
      - name: app
        image: nginx:1.27
```

`base/kustomization.yaml`:

```yaml
resources:
- deployment.yaml
```

`overlays/staging/kustomization.yaml`:

```yaml
resources:
- ../../base
replicas:
- name: catalog
  count: 3
labels:
- pairs:
    environment: staging
  includeTemplates: true
```

Apply with `kubectl apply -k overlays/staging`. Validate with `kubectl get deployment catalog -o jsonpath='{.spec.replicas}{" "}{.spec.template.metadata.labels.environment}'`; it must report `3 staging`.

## ✅ W-04: Deploy an existing Helm chart

```sh
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm install edge bitnami/nginx --namespace edge-demo --create-namespace --set replicaCount=2 --wait
```

Validate with `helm status edge -n edge-demo` and `kubectl get pods -n edge-demo`. The exact generated workload name is chart-version dependent; confirm it has two ready replicas.