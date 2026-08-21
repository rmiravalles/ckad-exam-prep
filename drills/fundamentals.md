# 🧱 Fundamentals Drills

## 🧪 F-01: Pod command and arguments

- **Difficulty:** Foundation
- **Target time:** 4 minutes
- **Scenario:** Create a Pod named `echo-once` using `busybox:1.36`. It must run `sh -c 'echo CKAD-ready; sleep 3600'` and remain running. Do not use a Deployment.
- **Expected outcome:** A running Pod whose logs contain `CKAD-ready`.
- **Common traps:** Treating the shell expression as separate command arguments; omitting the shell when using `-c`.