# 🩺 Troubleshooting Drills

## 🧪 T-01: CrashLoopBackOff

- **Difficulty:** Core
- **Target time:** 5 minutes
- **Scenario:** A Pod named `broken-command` uses `busybox:1.36` and is repeatedly restarting. Diagnose the cause with Kubernetes inspection commands, then correct the Pod so it prints `recovered` and remains running.
- **Expected outcome:** You identify the failing command from logs or Pod configuration and produce a running replacement Pod.
- **Common traps:** Editing before checking Events and logs; assuming the image is broken; fixing the symptom without identifying the exited process.

## 🧪 T-02: Service has no endpoints

- **Difficulty:** Core
- **Target time:** 6 minutes
- **Scenario:** A running Pod named `inventory` is labeled `app=inventory`. A ClusterIP Service named `inventory` has no endpoints. Diagnose the selector mismatch using Kubernetes inspection commands, then correct the Service so it selects the Pod on port `80` and targets port `8080`.
- **Expected outcome:** You identify the mismatch before editing, and `kubectl get endpoints inventory` lists the ready Pod.
- **Common traps:** Changing Pod labels before inspecting the Service selector; assuming `containerPort` creates endpoints; validating the Service object but not its endpoints.

## 🧪 T-03: Readiness probe blocks traffic

- **Difficulty:** Core
- **Target time:** 7 minutes
- **Scenario:** A Pod named `unready-web` is running but absent from Service endpoints. Diagnose the readiness failure with `describe` and logs, then correct the probe so it checks an HTTP application listening on port `8080` at `/healthz`.
- **Expected outcome:** You identify the failing readiness configuration and produce a ready Pod that becomes a Service endpoint.
- **Common traps:** Replacing readiness with liveness; changing the Service selector before examining Pod readiness; editing before reviewing Events.