# Troubleshooting Drills

## T-01: CrashLoopBackOff

- **Difficulty:** Core
- **Target time:** 5 minutes
- **Scenario:** A Pod named `broken-command` uses `busybox:1.36` and is repeatedly restarting. Diagnose the cause with Kubernetes inspection commands, then correct the Pod so it prints `recovered` and remains running.
- **Expected outcome:** You identify the failing command from logs or Pod configuration and produce a running replacement Pod.
- **Common traps:** Editing before checking Events and logs; assuming the image is broken; fixing the symptom without identifying the exited process.