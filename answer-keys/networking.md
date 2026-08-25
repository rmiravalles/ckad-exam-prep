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

## ✅ N-02: Ingress path routing

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: catalog
spec:
  ingressClassName: nginx
  rules:
  - host: catalog.example.com
    http:
      paths:
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: catalog
            port:
              number: 80
```

Validate with `kubectl describe ingress catalog`. This checks the Ingress resource; request routing also requires an installed `nginx` Ingress controller.

## ✅ N-03: Default-deny ingress NetworkPolicy

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-ingress
  namespace: team-a
spec:
  podSelector: {}
  policyTypes:
  - Ingress
```

Validate with `kubectl get networkpolicy deny-ingress -n team-a -o yaml`. Enforcement requires a network plugin that implements NetworkPolicy.