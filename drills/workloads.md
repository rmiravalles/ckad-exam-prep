# Workload Drills

## W-01: Deployment with container port

- **Difficulty:** Core
- **Target time:** 6 minutes
- **Scenario:** Create a Deployment named `web` with three replicas. Each Pod must run `nginx:1.27`, expose container port `8080`, and carry the label `app=web`.
- **Expected outcome:** The Deployment has three available replicas and its selector matches the Pod-template labels.
- **Common traps:** Selector and template-label mismatch; putting `ports` at the Pod level; omitting `replicas`.