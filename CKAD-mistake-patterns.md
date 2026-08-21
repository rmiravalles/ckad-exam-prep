# CKAD Mistake Patterns

Promote a session-log entry here only when it recurs or reveals a missing mental model. Each pattern should end with a fresh repair drill.

## Labels and selectors do not match

- **Symptom:** A Service has no endpoints, or a Deployment creates no matching Pods.
- **Mental model:** Selectors are exact label queries; Kubernetes does not infer relationships from names.
- **Correction:** Compare every selector key and value to the selected resource's labels.
- **Repair drill:** Create a Deployment and ClusterIP Service, then verify the Service has endpoints.

## `command` and `args` are confused

- **Symptom:** A container starts the wrong process or exits immediately.
- **Mental model:** `command` replaces an image's entrypoint; `args` replaces its default command arguments.
- **Correction:** Inspect the image defaults or state explicitly which part must be overridden.
- **Repair drill:** Run one Pod that replaces only arguments and one that replaces the command and arguments.

## `port` and `targetPort` are confused

- **Symptom:** A Service exists but cannot reach the container.
- **Mental model:** `port` is the Service-facing port; `targetPort` is the selected Pod's port or named port.
- **Correction:** Verify the target resolves to the container's listening port.
- **Repair drill:** Expose a container listening on `8080` through a Service on `80`.

## A probe is treated as a generic health check

- **Symptom:** Traffic reaches an unready Pod, or Kubernetes restarts a slow-starting container.
- **Mental model:** Readiness controls endpoint eligibility; liveness triggers restarts; startup protects slow initialization.
- **Correction:** State the operational consequence before choosing the probe type.
- **Repair drill:** Add distinct readiness and liveness HTTP probes, then explain the failure result of each.

## Job restart policy is invalid

- **Symptom:** The API rejects a Job manifest.
- **Mental model:** Job Pod templates support `Never` and `OnFailure`, not `Always`.
- **Correction:** Set `restartPolicy` in the Job template, not at an unrelated level.
- **Repair drill:** Create a one-shot Job and verify it reaches completion.

## Volume names do not connect

- **Symptom:** A Pod is rejected because a mount references an unknown volume.
- **Mental model:** `volumeMounts[].name` and `volumes[].name` are the exact join key.
- **Correction:** Trace the name from the container mount to the Pod volume source.
- **Repair drill:** Mount a PVC at `/data` and confirm the claim is bound.