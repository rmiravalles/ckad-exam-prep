# ✅ CKAD Validation Checklist

Use these checks after creating or changing a resource. Verify the intended behavior, not only that a manifest was accepted.

## 🔎 General

- Run `kubectl apply -f FILE.yaml` and inspect the returned resource names.
- Run `kubectl get RESOURCE NAME -o yaml` to confirm the effective configuration.
- Run `kubectl describe RESOURCE NAME` before editing when behavior differs from expectation.
- Check Events in `kubectl describe` for scheduling, image, volume, selector, and probe failures.

## 📦 Pods and containers

- Confirm status with `kubectl get pod NAME -o wide`.
- Inspect container output with `kubectl logs NAME [-c CONTAINER]`.
- Check process-level behavior with `kubectl exec -it NAME [-c CONTAINER] -- sh` when the image provides a shell.
- For commands, arguments, environment variables, and mounts, inspect the Pod YAML and test the value from inside the container.

## 🔁 Deployments and ReplicaSets

- Run `kubectl rollout status deployment/NAME`.
- Confirm desired, current, and available replicas with `kubectl get deployment NAME`.
- Verify the selector exactly matches the Pod template labels.
- Inspect created Pods with `kubectl get pods -l KEY=VALUE`.

## 🌐 Services and networking

- Confirm the selector and ports with `kubectl describe service NAME`.
- Verify backing endpoints with `kubectl get endpoints NAME`.
- Ensure the Service selector matches labels on ready Pods.
- Test name resolution or connectivity from a temporary debug Pod when the scenario requires it.

## 🔐 ConfigMaps, Secrets, and volumes

- Inspect keys with `kubectl describe configmap NAME` or `kubectl describe secret NAME`.
- Confirm environment injection or mounted files from inside the running container.
- Check `volumeMounts` names against `volumes` names exactly.
- For PVCs, confirm `kubectl get pvc NAME` shows `Bound` before expecting a mounted Pod to start.

## ⏱️ Probes, Jobs, and CronJobs

- Inspect probe configuration in the Pod YAML and Events for failures or restarts.
- Check Job completion with `kubectl get jobs` and logs from its Pod.
- Confirm a CronJob's schedule and Job template with `kubectl describe cronjob NAME`.
- Ensure Job Pods use an allowed `restartPolicy`, typically `Never` or `OnFailure`.

## 🛡️ Security and troubleshooting

- Confirm the service account with `kubectl get pod NAME -o jsonpath='{.spec.serviceAccountName}'`.
- Inspect security context fields in the effective Pod YAML.
- Start diagnosis with `get`, then `describe`, then `logs`, then `exec`; avoid editing before evidence points to a cause.