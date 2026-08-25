# Manifest and Validation Reference

Use this only after attempting a drill. Verify intended behavior, not merely that Kubernetes accepted the manifest.

## General validation

- Run `kubectl apply -f FILE.yaml`, then inspect the effective resource with `kubectl get RESOURCE NAME -o yaml`.
- Check Events in `kubectl describe RESOURCE NAME` for scheduling, image, volume, selector, and probe failures.
- For Pods, use `get`, `describe`, `logs`, and `exec` to confirm commands, arguments, environment variables, and mounts.
- For Deployments, run `kubectl rollout status deployment/NAME`, verify replica counts, and confirm selectors match Pod-template labels.
- For Services, inspect selectors and ports, then verify endpoints with `kubectl get endpoints NAME`.
- For ConfigMaps, Secrets, and volumes, check referenced names and keys exactly. Confirm a PVC is `Bound` before expecting its Pod to start.
- For Jobs and CronJobs, inspect completion, logs, schedule, and the Job template's `restartPolicy`.
- For service accounts and security contexts, inspect the effective Pod YAML.

## Minimal manifest patterns

### Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sample-pod
spec:
  containers:
  - name: app
    image: nginx
```

### Deployment and Service

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sample-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: sample
  template:
    metadata:
      labels:
        app: sample
    spec:
      containers:
      - name: app
        image: nginx
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: sample-svc
spec:
  type: ClusterIP
  selector:
    app: sample
  ports:
  - port: 80
    targetPort: 80
```

### Configuration

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: sample-cm
data:
  LOG_LEVEL: debug
---
apiVersion: v1
kind: Secret
metadata:
  name: sample-secret
type: Opaque
stringData:
  PASSWORD: s3cr3t
```

Reference a ConfigMap with `configMapKeyRef` or a Secret with `secretKeyRef` from a container `env` entry. Match the object name and key exactly.

### Job and CronJob

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: sample-job
spec:
  template:
    spec:
      restartPolicy: Never
      containers:
      - name: app
        image: busybox
        command: ["sh", "-c", "echo hello"]
---
apiVersion: batch/v1
kind: CronJob
metadata:
  name: sample-cron
spec:
  schedule: "*/5 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          restartPolicy: OnFailure
          containers:
          - name: app
            image: busybox
            command: ["sh", "-c", "date"]
```

### PVC and mount

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: sample-pvc
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
  name: pvc-pod
spec:
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - name: data
      mountPath: /data
  volumes:
  - name: data
    persistentVolumeClaim:
      claimName: sample-pvc
```

### Liveness and readiness probes

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: probe-pod
spec:
  containers:
  - name: app
    image: nginx
    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
    readinessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 3
      periodSeconds: 5
```