# 🔑 Configuration Answer Keys

## ✅ C-01: ConfigMap environment variable

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-settings
data:
  LOG_LEVEL: info
---
apiVersion: v1
kind: Pod
metadata:
  name: settings-reader
spec:
  containers:
  - name: app
    image: busybox:1.36
    command: ["sh", "-c", "sleep 3600"]
    env:
    - name: LOG_LEVEL
      valueFrom:
        configMapKeyRef:
          name: app-settings
          key: LOG_LEVEL
```

Validate with `kubectl exec settings-reader -- printenv LOG_LEVEL`.

## ✅ C-02: Secret mounted as a file

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-credentials
type: Opaque
stringData:
  username: appuser
  password: change-me
---
apiVersion: v1
kind: Pod
metadata:
  name: credential-reader
spec:
  containers:
  - name: app
    image: busybox:1.36
    command: ["sh", "-c", "sleep 3600"]
    volumeMounts:
    - name: credentials
      mountPath: /etc/credentials
      readOnly: true
  volumes:
  - name: credentials
    secret:
      secretName: db-credentials
      items:
      - key: username
        path: user
```

Validate with `kubectl exec credential-reader -- cat /etc/credentials/user` and `kubectl exec credential-reader -- ls /etc/credentials`.

## ✅ C-03: Resource requests and limits

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: bounded
spec:
  containers:
  - name: app
    image: busybox:1.36
    command: ["sh", "-c", "sleep 3600"]
    resources:
      requests:
        cpu: 100m
        memory: 64Mi
      limits:
        cpu: 250m
        memory: 128Mi
```

Validate with `kubectl get pod bounded -o jsonpath='{.spec.containers[0].resources}'`.