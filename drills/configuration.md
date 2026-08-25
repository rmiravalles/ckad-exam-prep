# 🔐 Configuration Drills

## 🧪 C-01: ConfigMap environment variable

- **Difficulty:** Core
- **Target time:** 6 minutes
- **Scenario:** Create a ConfigMap named `app-settings` with `LOG_LEVEL=info`. Create a Pod named `settings-reader` using `busybox:1.36` that stays running and receives `LOG_LEVEL` from that ConfigMap key as an environment variable.
- **Expected outcome:** The Pod is running and `kubectl exec settings-reader -- printenv LOG_LEVEL` returns `info`.
- **Common traps:** Using the wrong key; placing `valueFrom` at the wrong level; forgetting a long-running command.

## 🧪 C-02: Secret mounted as a file

- **Difficulty:** Core
- **Target time:** 6 minutes
- **Scenario:** Create an Opaque Secret named `db-credentials` with `username=appuser` and `password=change-me`. Create a Pod named `credential-reader` using `busybox:1.36` that mounts only the `username` key as `/etc/credentials/user` and remains running.
- **Expected outcome:** `kubectl exec credential-reader -- cat /etc/credentials/user` returns `appuser`, and the password is not mounted.
- **Common traps:** Base64-encoding values when using `stringData`; mounting every Secret key; confusing the projected file path with `mountPath`.

## 🧪 C-03: Resource requests and limits

- **Difficulty:** Core
- **Target time:** 5 minutes
- **Scenario:** Create a Pod named `bounded` using `busybox:1.36` that remains running. Its container must request `100m` CPU and `64Mi` memory, and be limited to `250m` CPU and `128Mi` memory.
- **Expected outcome:** The effective Pod specification contains all four values under the container's `resources` section.
- **Common traps:** Putting resources at the Pod level; swapping requests and limits; using invalid units.