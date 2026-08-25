# 🔑 Storage and Security Answer Keys

## ✅ SS-01: PVC and Pod mount

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cache
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: cache-writer
spec:
  containers:
  - name: app
    image: busybox:1.36
    command: ["sh", "-c", "sleep 3600"]
    volumeMounts:
    - name: cache
      mountPath: /cache
  volumes:
  - name: cache
    persistentVolumeClaim:
      claimName: cache
```

Validate with `kubectl get pvc cache`, then `kubectl describe pod cache-writer`.

## ✅ SS-02: Pod security context

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: restricted-app
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 1000
    fsGroup: 2000
  containers:
  - name: app
    image: busybox:1.36
    command: ["sh", "-c", "sleep 3600"]
    securityContext:
      allowPrivilegeEscalation: false
      capabilities:
        drop:
        - ALL
```

Validate with `kubectl get pod restricted-app -o yaml` and inspect both `securityContext` sections.

## ✅ SS-03: Service account assignment

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: reporter
---
apiVersion: v1
kind: Pod
metadata:
  name: reporter
spec:
  serviceAccountName: reporter
  automountServiceAccountToken: false
  containers:
  - name: app
    image: busybox:1.36
    command: ["sh", "-c", "sleep 3600"]
```

Validate with `kubectl get pod reporter -o jsonpath='{.spec.serviceAccountName}{" "}{.spec.automountServiceAccountToken}'`.