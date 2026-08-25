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
| C-01 | ConfigMaps and Secrets | Core | 6 min | F-01 | [Configuration](configuration.md#c-01-configmap-environment-variable) | [Configuration](../answer-keys/configuration.md#c-01-configmap-environment-variable) |
| W-01 | Deployments | Core | 6 min | F-01 | [Workloads](workloads.md#w-01-deployment-with-container-port) | [Workloads](../answer-keys/workloads.md#w-01-deployment-with-container-port) |
| N-01 | Services and selectors | Core | 6 min | W-01 | [Networking](networking.md#n-01-clusterip-service) | [Networking](../answer-keys/networking.md#n-01-clusterip-service) |
| SS-01 | PVCs and volume mounts | Core | 7 min | F-01 | [Storage and security](storage-security.md#ss-01-pvc-and-pod-mount) | [Storage and security](../answer-keys/storage-security.md#ss-01-pvc-and-pod-mount) |
| T-01 | Pod diagnosis | Core | 5 min | F-01 | [Troubleshooting](troubleshooting.md#t-01-crashloopbackoff) | [Troubleshooting](../answer-keys/troubleshooting.md#t-01-crashloopbackoff) |
| M-01 | Mixed fundamentals | Timed | 20 min | F-01 through SS-01 | [Timed simulations](timed-simulations.md#m-01-mixed-fundamentals) | [Timed simulations](../answer-keys/timed-simulations.md#m-01-mixed-fundamentals) |

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