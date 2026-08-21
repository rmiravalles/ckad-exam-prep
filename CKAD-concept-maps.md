# CKAD Concept Maps

Use these compact maps when a repeated miss shows that syntax is present but the underlying behavior is not.

## Workload to network traffic

```text
Deployment selector -> Pod-template labels -> ready Pods
Service selector -> matching ready Pods -> Endpoints -> traffic to targetPort
```

The Deployment and Service selectors are independent. They must each match the labels they select.

## Container startup

```text
Image defaults
  + command (replaces entrypoint)
  + args (replaces default arguments)
  + environment and mounts
  -> container process
```

An immediately exiting process can cause restart loops depending on the Pod restart policy.

## Configuration delivery

```text
ConfigMap or Secret
  -> env / envFrom
  -> key reference
  -> mounted volume files
```

Choose environment variables for process configuration and mounted files when the application expects files. Confirm names and keys exactly.

## Health and availability

```text
startupProbe protects initialization
readinessProbe controls Service endpoint eligibility
livenessProbe restarts an unhealthy container
```

These probes answer different operational questions and should not be used interchangeably.

## Persistent storage

```text
PVC request -> matching storage -> PVC bound
Pod volume references claim -> container volumeMount references volume name -> mounted path
```

The PVC must bind, and the volume name must exactly match the container's mount name.