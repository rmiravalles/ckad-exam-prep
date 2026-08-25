# 🧱 Fundamentals Drills

## 🧪 F-01: Pod command and arguments

- **Difficulty:** Foundation
- **Target time:** 4 minutes
- **Scenario:** Create a Pod named `echo-once` using `busybox:1.36`. It must run `sh -c 'echo CKAD-ready; sleep 3600'` and remain running. Do not use a Deployment.
- **Expected outcome:** A running Pod whose logs contain `CKAD-ready`.
- **Common traps:** Treating the shell expression as separate command arguments; omitting the shell when using `-c`.

## 🧪 F-02: Init container and shared volume

- **Difficulty:** Core
- **Target time:** 7 minutes
- **Scenario:** Create a Pod named `prepared-app` using `busybox:1.36`. An init container named `prepare` must write `ready` to `/work/status` in a shared `emptyDir` volume. The application container named `reader` must wait until the file exists, print its contents, and remain running.
- **Expected outcome:** The init container completes before `reader` starts, and `kubectl logs prepared-app -c reader` contains `ready`.
- **Common traps:** Mounting the volume in only one container; putting `initContainers` under `containers`; assuming containers in a Pod run sequentially without an init container.

## 🧪 F-03: Sidecar log tailer

- **Difficulty:** Core
- **Target time:** 7 minutes
- **Scenario:** Create a Pod named `log-producer` with two `busybox:1.36` containers sharing an `emptyDir` volume mounted at `/var/log/app`. Container `writer` must append a timestamped line to `/var/log/app/app.log` every five seconds. Container `tailer` must stream that file to its standard output.
- **Expected outcome:** Both containers are running and `kubectl logs log-producer -c tailer` shows lines written by `writer`.
- **Common traps:** Using separate volumes; failing when the log file does not exist yet; allowing either container to exit.