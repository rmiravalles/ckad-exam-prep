# 📄 CKAD Sample Manifests

## 📦 Pod
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

## 🔁 Deployment
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
```

## 🌐 Service
```yaml
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

## 🔐 ConfigMap + Pod env
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: sample-cm
data:
  LOG_LEVEL: debug
---
apiVersion: v1
kind: Pod
metadata:
  name: cm-pod
spec:
  containers:
  - name: app
    image: nginx
    env:
    - name: LOG_LEVEL
      valueFrom:
        configMapKeyRef:
          name: sample-cm
          key: LOG_LEVEL
```

## 🔒 Secret + Pod env
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: sample-secret
type: Opaque
stringData:
  PASSWORD: s3cr3t
---
apiVersion: v1
kind: Pod
metadata:
  name: secret-pod
spec:
  containers:
  - name: app
    image: nginx
    env:
    - name: PASSWORD
      valueFrom:
        secretKeyRef:
          name: sample-secret
          key: PASSWORD
```

## ✅ Job
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
```

## ⏱️ CronJob
```yaml
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

## 💾 PVC
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
```

## 💾 Pod with PVC
```yaml
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

## 🩺 Pod with liveness/readiness probes
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
