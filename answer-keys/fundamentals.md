# Fundamentals Answer Keys

## F-01: Pod command and arguments

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