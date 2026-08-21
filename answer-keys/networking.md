# 🔑 Networking Answer Keys

## ✅ N-01: ClusterIP Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web
spec:
  type: ClusterIP
  selector:
    app: web
  ports:
  - port: 80
    targetPort: 8080
```

Validate with `kubectl get endpoints web` after matching, ready Pods exist.

Note: Endpoint presence validates selector matching. End-to-end traffic also requires the workload to listen on the target port.