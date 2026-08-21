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