# 🌐 Networking Drills

## 🧪 N-01: ClusterIP Service

- **Difficulty:** Core
- **Target time:** 6 minutes
- **Scenario:** Expose Pods labeled `app=web` with a ClusterIP Service named `web`. The Service must listen on port `80` and forward to container port `8080`.
- **Expected outcome:** `kubectl get endpoints web` lists the ready backend Pods.
- **Common traps:** Selecting the Deployment name rather than Pod labels; confusing `port` and `targetPort`; failing to check endpoints.