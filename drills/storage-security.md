# Storage and Security Drills

## SS-01: PVC and Pod mount

- **Difficulty:** Core
- **Target time:** 7 minutes
- **Scenario:** Create a PVC named `cache` requesting `1Gi` with `ReadWriteOnce`. Create a Pod named `cache-writer` using `busybox:1.36` that mounts the claim at `/cache` and remains running.
- **Expected outcome:** The PVC is bound and the Pod mount is visible in the effective Pod specification.
- **Common traps:** Mismatched volume and mount names; using a PersistentVolume rather than a claim; not waiting for the claim to bind.