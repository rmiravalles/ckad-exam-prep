# 🔐 Configuration Drills

## 🧪 C-01: ConfigMap environment variable

- **Difficulty:** Core
- **Target time:** 6 minutes
- **Scenario:** Create a ConfigMap named `app-settings` with `LOG_LEVEL=info`. Create a Pod named `settings-reader` using `busybox:1.36` that stays running and receives `LOG_LEVEL` from that ConfigMap key as an environment variable.
- **Expected outcome:** The Pod is running and `kubectl exec settings-reader -- printenv LOG_LEVEL` returns `info`.
- **Common traps:** Using the wrong key; placing `valueFrom` at the wrong level; forgetting a long-running command.