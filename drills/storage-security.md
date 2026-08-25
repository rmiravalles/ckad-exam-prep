# 🛡️ Storage and Security Drills

## 🧪 SS-01: PVC and Pod mount

- **Difficulty:** Core
- **Target time:** 7 minutes
- **Scenario:** Create a PVC named `cache` requesting `1Gi` with `ReadWriteOnce`. Create a Pod named `cache-writer` using `busybox:1.36` that mounts the claim at `/cache` and remains running.
- **Expected outcome:** The PVC is bound and the Pod mount is visible in the effective Pod specification.
- **Common traps:** Mismatched volume and mount names; using a PersistentVolume rather than a claim; not waiting for the claim to bind.

## 🧪 SS-02: Pod security context

- **Difficulty:** Core
- **Target time:** 7 minutes
- **Scenario:** Create a Pod named `restricted-app` using `busybox:1.36` that remains running. Configure the Pod to run as user and group `1000`, set `fsGroup` to `2000`, and configure the container to disallow privilege escalation while dropping every Linux capability.
- **Expected outcome:** The Pod and container security-context fields match the requested restrictions in the effective specification.
- **Common traps:** Putting Pod-level fields under the container security context; using `capabilities.drop` as a string; confusing `runAsGroup` with `fsGroup`.

## 🧪 SS-03: Service account assignment

- **Difficulty:** Core
- **Target time:** 5 minutes
- **Scenario:** Create a ServiceAccount named `reporter`. Create a Pod named `reporter` using `busybox:1.36` that remains running and uses that ServiceAccount. Disable automatic mounting of the service-account token for this Pod.
- **Expected outcome:** The Pod uses `reporter` and has `automountServiceAccountToken: false` in its effective specification.
- **Common traps:** Creating the ServiceAccount but not assigning it to the Pod; using the wrong field name; placing the token setting under the container.