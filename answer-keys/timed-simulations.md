# 🔑 Timed Simulation Answer Keys

## ✅ M-01: Mixed fundamentals

Use the answer keys for [W-01](workloads.md#w-01-deployment-with-container-port), [N-01](networking.md#n-01-clusterip-service), and [C-01](configuration.md#c-01-configmap-environment-variable) as the reference components.

For the final Deployment, inject the ConfigMap key into the container environment:

```yaml
env:
- name: LOG_LEVEL
  valueFrom:
    configMapKeyRef:
      name: app-settings
      key: LOG_LEVEL
```

Validate rollout status, Service endpoints, and the environment variable in one ready Pod. Record whether the workload's actual listener matches the Service target port before attempting an end-to-end HTTP request.