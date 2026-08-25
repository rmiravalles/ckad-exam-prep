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

## 🧪 M-02: Secure application delivery

- **Difficulty:** Timed
- **Target time:** 30 minutes
- **Scenario:** In namespace `checkout`, complete the following without opening answer keys:
  1. Create Secret `checkout-db` containing `DATABASE_URL=postgres://checkout:change-me@db:5432/checkout`.
  2. Create a two-replica Deployment `checkout` using `nginx:1.27`, labeled `app=checkout`, with the Secret injected as `DATABASE_URL`, CPU request `100m`, and memory limit `128Mi`.
  3. Expose it with a ClusterIP Service named `checkout` on port `80` targeting `80`.
  4. Add an Ingress named `checkout` using class `nginx` for `checkout.example.com` and path `/`.
  5. Create a default-deny ingress NetworkPolicy for the namespace.
- **Expected outcome:** All resources exist with consistent labels and configuration. The Service has endpoints before the NetworkPolicy is evaluated by a supporting CNI.
- **Common traps:** Forgetting namespace scoping; opening answer keys during implementation; assuming NetworkPolicy behavior is enforced on a cluster without a supporting network plugin.