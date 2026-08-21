# ⏱️ Timed Simulations

## 🧪 M-01: Mixed fundamentals

- **Difficulty:** Timed
- **Target time:** 20 minutes
- **Scenario:** In a dedicated namespace, complete the following without consulting answer keys:
  1. Create the `web` Deployment from W-01.
  2. Create the `web` ClusterIP Service from N-01.
  3. Create the `app-settings` ConfigMap from C-01.
  4. Add `LOG_LEVEL` from `app-settings` to the Deployment's containers.
  5. Verify that the Service has endpoints and that a running application Pod receives `LOG_LEVEL=info`.
- **Expected outcome:** All resources exist, the Deployment is available, the Service has endpoints, and the environment variable is injected.
- **Common traps:** Losing selector consistency while patching; verifying only resource creation instead of behavior; spending too long hand-writing boilerplate.