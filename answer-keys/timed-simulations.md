# 🔑 Timed Simulation Answer Keys

## ✅ M-01: Mixed fundamentals

Use the answer keys for [W-01](workloads.md#w-01-deployment-with-container-port), [N-01](networking.md#n-01-clusterip-service), and [C-01](configuration.md#c-01-configmap-environment-variable) as the reference components.

For the final Deployment, inject the ConfigMap key into the container environment:

```yaml
env:
- name: LOG_LEVEL
  valueFrom:
    configMapKeyRef:
      name: app-settings
      key: LOG_LEVEL
```

Validate rollout status, Service endpoints, and the environment variable in one ready Pod. Record whether the workload's actual listener matches the Service target port before attempting an end-to-end HTTP request.

## ✅ M-02: Secure application delivery

Create the namespace first:

```sh
kubectl create namespace checkout
```

Apply this manifest:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: checkout-db
  namespace: checkout
type: Opaque
stringData:
  DATABASE_URL: postgres://checkout:change-me@db:5432/checkout
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: checkout
  namespace: checkout
spec:
  replicas: 2
  selector:
    matchLabels:
      app: checkout
  template:
    metadata:
      labels:
        app: checkout
    spec:
      containers:
      - name: app
        image: nginx:1.27
        env:
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: checkout-db
              key: DATABASE_URL
        resources:
          requests:
            cpu: 100m
          limits:
            memory: 128Mi
---
apiVersion: v1
kind: Service
metadata:
  name: checkout
  namespace: checkout
spec:
  selector:
    app: checkout
  ports:
  - port: 80
    targetPort: 80
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: checkout
  namespace: checkout
spec:
  ingressClassName: nginx
  rules:
  - host: checkout.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: checkout
            port:
              number: 80
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-ingress
  namespace: checkout
spec:
  podSelector: {}
  policyTypes:
  - Ingress
```

Validate with `kubectl rollout status deployment/checkout -n checkout`, `kubectl get endpoints checkout -n checkout`, and `kubectl get ingress,networkpolicy -n checkout`. Ingress routing and NetworkPolicy enforcement require cluster controllers that support them.