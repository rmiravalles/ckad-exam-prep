# 🔑 Troubleshooting Answer Keys

## ✅ T-01: CrashLoopBackOff

Start with evidence:

```sh
kubectl describe pod broken-command
kubectl logs broken-command --previous
```

A valid repair creates a Pod whose process stays alive after printing the required output:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: broken-command
spec:
  containers:
  - name: app
    image: busybox:1.36
    command: ["sh", "-c", "echo recovered; sleep 3600"]
```

Validate with `kubectl get pod broken-command` and `kubectl logs broken-command`.

## ✅ T-02: Service has no endpoints

Start with evidence:

```sh
kubectl get pod inventory --show-labels
kubectl describe service inventory
kubectl get endpoints inventory
```

The Service selector must match the Pod label. A valid repair is:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: inventory
spec:
  type: ClusterIP
  selector:
    app: inventory
  ports:
  - port: 80
    targetPort: 8080
```

Validate with `kubectl get endpoints inventory`. Endpoint creation is based on selector matching and ready Pods, not on the declared `containerPort` field.

## ✅ T-03: Readiness probe blocks traffic

Start with evidence:

```sh
kubectl describe pod unready-web
kubectl logs unready-web
kubectl get pod unready-web -o jsonpath='{.status.conditions[?(@.type=="Ready")].status}'
```

A valid repaired Pod, assuming the Service selects `app=unready-web`, is:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: unready-web
  labels:
    app: unready-web
spec:
  containers:
  - name: app
    image: hashicorp/http-echo:1.0.0
    args:
    - -text=ready
    - -listen=:8080
    readinessProbe:
      httpGet:
        path: /healthz
        port: 8080
      initialDelaySeconds: 1
      periodSeconds: 3
```

Validate with `kubectl get pod unready-web`, `kubectl describe pod unready-web`, and `kubectl get endpoints SERVICE_NAME`. Any HTTP path returns a successful response from this image.