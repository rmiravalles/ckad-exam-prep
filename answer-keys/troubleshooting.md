# Troubleshooting Answer Keys

## T-01: CrashLoopBackOff

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