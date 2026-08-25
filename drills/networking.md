# 🌐 Networking Drills

## 🧪 N-01: ClusterIP Service

- **Difficulty:** Core
- **Target time:** 6 minutes
- **Scenario:** Expose Pods labeled `app=web` with a ClusterIP Service named `web`. The Service must listen on port `80` and forward to container port `8080`.
- **Expected outcome:** `kubectl get endpoints web` lists the ready backend Pods.
- **Common traps:** Selecting the Deployment name rather than Pod labels; confusing `port` and `targetPort`; failing to check endpoints.

## 🧪 N-02: Ingress path routing

- **Difficulty:** Core
- **Target time:** 8 minutes
- **Scenario:** A Service named `catalog` exists on port `80`. Create an Ingress named `catalog` using ingress class `nginx` that routes requests for host `catalog.example.com` and path `/api` with `Prefix` matching to that Service and port.
- **Expected outcome:** The effective Ingress specification contains the class, host, path type, backend Service name, and backend Service port.
- **Common traps:** Using the obsolete backend service syntax; omitting `pathType`; specifying a container port rather than the Service port.

## 🧪 N-03: Default-deny ingress NetworkPolicy

- **Difficulty:** Core
- **Target time:** 7 minutes
- **Scenario:** In namespace `team-a`, create a NetworkPolicy named `deny-ingress` that selects every Pod and denies all inbound traffic while leaving egress unaffected.
- **Expected outcome:** The policy has an empty Pod selector and `Ingress` as its only policy type.
- **Common traps:** Adding an empty ingress rule, which allows ingress; accidentally adding `Egress` to `policyTypes`; using labels that select only some Pods.