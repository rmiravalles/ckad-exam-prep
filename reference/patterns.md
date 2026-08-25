# CKAD Repair Patterns

Use these after a repeated miss. Each pattern states the mental model and ends with a fresh repair drill.

## Workload to network traffic

```text
Deployment selector -> Pod-template labels -> ready Pods
Service selector -> matching ready Pods -> Endpoints -> traffic to targetPort
```

Deployment and Service selectors are independent. Each must match the labels it selects.

**Failure: labels and selectors do not match**

- Symptom: a Service has no endpoints, or a Deployment creates no matching Pods.
- Correction: compare every selector key and value to the selected resource's labels.
- Repair drill: create a Deployment and ClusterIP Service, then verify that the Service has endpoints.

## Container startup

```text
Image defaults + command (replaces entrypoint) + args (replaces default arguments)
  + environment and mounts -> container process
```

An immediately exiting process can cause restart loops depending on the Pod restart policy.

**Failure: `command` and `args` are confused**

- Symptom: a container starts the wrong process or exits immediately.
- Correction: state explicitly which image default is being replaced.
- Repair drill: run one Pod that replaces only arguments and one that replaces both command and arguments.

## Configuration delivery

```text
ConfigMap or Secret -> env / envFrom / mounted volume files
```

Choose environment variables for process configuration and mounted files when the application expects files. Confirm names and keys exactly.

## Health and availability

```text
startupProbe protects initialization
readinessProbe controls Service endpoint eligibility
livenessProbe restarts an unhealthy container
```

**Failure: a probe is treated as a generic health check**

- Symptom: traffic reaches an unready Pod, or Kubernetes restarts a slow-starting container.
- Correction: state the operational consequence before choosing the probe type.
- Repair drill: add distinct readiness and liveness HTTP probes, then explain the failure result of each.

## Services

**Failure: `port` and `targetPort` are confused**

- Symptom: a Service exists but cannot reach the container.
- Mental model: `port` is the Service-facing port; `targetPort` is the selected Pod's port or named port.
- Correction: verify that the target resolves to the container's listening port.
- Repair drill: expose a container listening on `8080` through a Service on `80`.

## Jobs

**Failure: Job restart policy is invalid**

- Symptom: the API rejects a Job manifest.
- Mental model: Job Pod templates support `Never` and `OnFailure`, not `Always`.
- Correction: set `restartPolicy` in the Job template.
- Repair drill: create a one-shot Job and verify it reaches completion.

## Persistent storage

```text
PVC request -> matching storage -> PVC bound
Pod volume references claim -> container volumeMount references volume name -> mounted path
```

**Failure: volume names do not connect**

- Symptom: a Pod is rejected because a mount references an unknown volume.
- Correction: trace the exact name from the container mount to the Pod volume source.
- Repair drill: mount a PVC at `/data` and confirm the claim is bound.