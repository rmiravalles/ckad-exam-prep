# 🔑 Fundamentals Answer Keys

## ✅ F-01: Pod command and arguments

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: echo-once
spec:
  containers:
  - name: app
    image: busybox:1.36
    command: ["sh", "-c"]
    args: ["echo CKAD-ready; sleep 3600"]
```

Validate with `kubectl get pod echo-once` and `kubectl logs echo-once`.

Valid alternative: put the entire invocation in `command`, provided `sh -c` receives the expression correctly.

## ✅ F-02: Init container and shared volume

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: prepared-app
spec:
  initContainers:
  - name: prepare
    image: busybox:1.36
    command: ["sh", "-c", "echo ready > /work/status"]
    volumeMounts:
    - name: work
      mountPath: /work
  containers:
  - name: reader
    image: busybox:1.36
    command: ["sh", "-c", "cat /work/status; sleep 3600"]
    volumeMounts:
    - name: work
      mountPath: /work
  volumes:
  - name: work
    emptyDir: {}
```

Validate with `kubectl get pod prepared-app`, `kubectl get pod prepared-app -o jsonpath='{.status.initContainerStatuses[0].state.terminated.reason}'`, and `kubectl logs prepared-app -c reader`.

## ✅ F-03: Sidecar log tailer

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: log-producer
spec:
  containers:
  - name: writer
    image: busybox:1.36
    command: ["sh", "-c", "while true; do date >> /var/log/app/app.log; sleep 5; done"]
    volumeMounts:
    - name: logs
      mountPath: /var/log/app
  - name: tailer
    image: busybox:1.36
    command: ["sh", "-c", "touch /var/log/app/app.log; tail -f /var/log/app/app.log"]
    volumeMounts:
    - name: logs
      mountPath: /var/log/app
  volumes:
  - name: logs
    emptyDir: {}
```

Validate with `kubectl logs log-producer -c tailer` after one write interval.