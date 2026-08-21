# Configuration Answer Keys

## C-01: ConfigMap environment variable

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