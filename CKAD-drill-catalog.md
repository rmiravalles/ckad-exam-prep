# CKAD Drill Catalog

Use this catalog to select the next drill by topic, difficulty, time budget, and prerequisite. Keep each drill's prompt in `drills/` and its complete reference solution in `answer-keys/`.

| ID | Topic | Difficulty | Target time | Prerequisite | Prompt | Answer key |
| --- | --- | --- | --- | --- | --- | --- |
| F-01 | Pods and container basics | Foundation | 4 min | None | [Fundamentals](drills/fundamentals.md#f-01-pod-command-and-arguments) | [Fundamentals](answer-keys/fundamentals.md#f-01-pod-command-and-arguments) |
| C-01 | ConfigMaps and Secrets | Core | 6 min | F-01 | [Configuration](drills/configuration.md#c-01-configmap-environment-variable) | [Configuration](answer-keys/configuration.md#c-01-configmap-environment-variable) |
| W-01 | Deployments | Core | 6 min | F-01 | [Workloads](drills/workloads.md#w-01-deployment-with-container-port) | [Workloads](answer-keys/workloads.md#w-01-deployment-with-container-port) |
| N-01 | Services and selectors | Core | 6 min | W-01 | [Networking](drills/networking.md#n-01-clusterip-service) | [Networking](answer-keys/networking.md#n-01-clusterip-service) |
| SS-01 | PVCs and volume mounts | Core | 7 min | F-01 | [Storage and security](drills/storage-security.md#ss-01-pvc-and-pod-mount) | [Storage and security](answer-keys/storage-security.md#ss-01-pvc-and-pod-mount) |
| T-01 | Pod diagnosis | Core | 5 min | F-01 | [Troubleshooting](drills/troubleshooting.md#t-01-crashloopbackoff) | [Troubleshooting](answer-keys/troubleshooting.md#t-01-crashloopbackoff) |
| M-01 | Mixed fundamentals | Timed | 20 min | F-01 through SS-01 | [Timed simulations](drills/timed-simulations.md#m-01-mixed-fundamentals) | [Timed simulations](answer-keys/timed-simulations.md#m-01-mixed-fundamentals) |

## Maintenance rules

- Give every drill a stable ID using its domain prefix.
- Keep prompts zero-hint; place solutions and validation steps only in `answer-keys/`.
- Add a row here whenever a new drill is added.
- Raise difficulty by combining established concepts, not by hiding required information.