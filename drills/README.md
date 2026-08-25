# CKAD Drills

Start here. Choose a drill, attempt it from memory without hints, then open its matching answer key only to review the result. Repeat with fresh names and values until the pattern is reliable.

## Recommended progression

- [ ] Pods and container basics
- [ ] Commands, args, environment, and working directory
- [ ] Labels, selectors, and annotations
- [ ] ConfigMaps and Secrets
- [ ] Probes
- [ ] Multi-container Pods
- [ ] Deployments and ReplicaSets
- [ ] Services and networking
- [ ] Jobs and CronJobs
- [ ] PersistentVolumes and PVCs
- [ ] SecurityContext, service accounts, and RBAC
- [ ] Ingress and application exposure
- [ ] Troubleshooting and mixed drills
- [ ] Timed simulations

## First ten patterns

Use this sequence when beginning from scratch:

1. Create a Pod with one container using a given image and command.
2. Patch a Pod to add an environment variable from a ConfigMap.
3. Create a Deployment with a specific replica count and container port.
4. Expose an app with a ClusterIP Service.
5. Mount a ConfigMap into a Pod as files.
6. Add liveness and readiness probes to a container.
7. Create a Job that runs to completion.
8. Create a CronJob that runs on a schedule.
9. Create a Pod with an init container and shared `emptyDir` volume.
10. Create a PersistentVolumeClaim and mount it into a Pod.

## Drill catalog

| ID | Topic | Difficulty | Target time | Prerequisite | Prompt | Answer key |
| --- | --- | --- | --- | --- | --- | --- |
| F-01 | Pods and container basics | Foundation | 4 min | None | [Fundamentals](fundamentals.md#f-01-pod-command-and-arguments) | [Fundamentals](../answer-keys/fundamentals.md#f-01-pod-command-and-arguments) |
| F-02 | Multi-container Pods | Core | 7 min | F-01 | [Fundamentals](fundamentals.md#f-02-init-container-and-shared-volume) | [Fundamentals](../answer-keys/fundamentals.md#f-02-init-container-and-shared-volume) |
| F-03 | Multi-container Pod sidecars | Core | 7 min | F-02 | [Fundamentals](fundamentals.md#f-03-sidecar-log-tailer) | [Fundamentals](../answer-keys/fundamentals.md#f-03-sidecar-log-tailer) |
| C-01 | ConfigMaps and Secrets | Core | 6 min | F-01 | [Configuration](configuration.md#c-01-configmap-environment-variable) | [Configuration](../answer-keys/configuration.md#c-01-configmap-environment-variable) |
| C-02 | Secret volumes | Core | 6 min | C-01 | [Configuration](configuration.md#c-02-secret-mounted-as-a-file) | [Configuration](../answer-keys/configuration.md#c-02-secret-mounted-as-a-file) |
| C-03 | Resource requirements | Core | 5 min | F-01 | [Configuration](configuration.md#c-03-resource-requests-and-limits) | [Configuration](../answer-keys/configuration.md#c-03-resource-requests-and-limits) |
| W-01 | Deployments | Core | 6 min | F-01 | [Workloads](workloads.md#w-01-deployment-with-container-port) | [Workloads](../answer-keys/workloads.md#w-01-deployment-with-container-port) |
| W-02 | Deployment rollouts | Core | 8 min | W-01 | [Workloads](workloads.md#w-02-rolling-update-and-rollback) | [Workloads](../answer-keys/workloads.md#w-02-rolling-update-and-rollback) |
| W-03 | Kustomize | Core | 10 min | W-01 | [Workloads](workloads.md#w-03-kustomize-overlay) | [Workloads](../answer-keys/workloads.md#w-03-kustomize-overlay) |
| W-04 | Helm | Core | 8 min | W-01 | [Workloads](workloads.md#w-04-deploy-an-existing-helm-chart) | [Workloads](../answer-keys/workloads.md#w-04-deploy-an-existing-helm-chart) |
| N-01 | Services and selectors | Core | 6 min | W-01 | [Networking](networking.md#n-01-clusterip-service) | [Networking](../answer-keys/networking.md#n-01-clusterip-service) |
| N-02 | Ingress | Core | 8 min | N-01 | [Networking](networking.md#n-02-ingress-path-routing) | [Networking](../answer-keys/networking.md#n-02-ingress-path-routing) |
| N-03 | NetworkPolicies | Core | 7 min | N-01 | [Networking](networking.md#n-03-default-deny-ingress-networkpolicy) | [Networking](../answer-keys/networking.md#n-03-default-deny-ingress-networkpolicy) |
| SS-01 | PVCs and volume mounts | Core | 7 min | F-01 | [Storage and security](storage-security.md#ss-01-pvc-and-pod-mount) | [Storage and security](../answer-keys/storage-security.md#ss-01-pvc-and-pod-mount) |
| SS-02 | Security contexts | Core | 7 min | F-01 | [Storage and security](storage-security.md#ss-02-pod-security-context) | [Storage and security](../answer-keys/storage-security.md#ss-02-pod-security-context) |
| SS-03 | Service accounts | Core | 5 min | F-01 | [Storage and security](storage-security.md#ss-03-service-account-assignment) | [Storage and security](../answer-keys/storage-security.md#ss-03-service-account-assignment) |
| T-01 | Pod diagnosis | Core | 5 min | F-01 | [Troubleshooting](troubleshooting.md#t-01-crashloopbackoff) | [Troubleshooting](../answer-keys/troubleshooting.md#t-01-crashloopbackoff) |
| T-02 | Service diagnosis | Core | 6 min | N-01 | [Troubleshooting](troubleshooting.md#t-02-service-has-no-endpoints) | [Troubleshooting](../answer-keys/troubleshooting.md#t-02-service-has-no-endpoints) |
| T-03 | Probe diagnosis | Core | 7 min | N-01 | [Troubleshooting](troubleshooting.md#t-03-readiness-probe-blocks-traffic) | [Troubleshooting](../answer-keys/troubleshooting.md#t-03-readiness-probe-blocks-traffic) |
| M-01 | Mixed fundamentals | Timed | 20 min | F-01 through SS-01 | [Timed simulations](timed-simulations.md#m-01-mixed-fundamentals) | [Timed simulations](../answer-keys/timed-simulations.md#m-01-mixed-fundamentals) |
| M-02 | Secure application delivery | Timed | 30 min | C-03, N-03, SS-02 | [Timed simulations](timed-simulations.md#m-02-secure-application-delivery) | [Timed simulations](../answer-keys/timed-simulations.md#m-02-secure-application-delivery) |

## Add a drill

Keep prompts in this directory zero-hint and place complete solutions and validation steps in the matching file under `answer-keys/`. Give each drill a stable domain-prefixed ID and add it to the catalog above.

```text
ID:
Topic:
Difficulty:
Scenario:
Expected outcome:
Common traps:
Source / notes:
```

Raise difficulty by combining established concepts, not by hiding required information.