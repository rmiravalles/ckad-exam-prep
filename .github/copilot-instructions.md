# CKAD Exam Prep Instructions

## Validation

This is a Markdown and Kubernetes-manifest study repository; it has no build, test, lint, package-manager, or CI commands.

- Validate a manifest in a disposable namespace or cluster with `kubectl apply -f FILE.yaml`, then inspect its effective state with `kubectl get RESOURCE NAME -o yaml`.
- Use the validation command supplied by the matching answer key for a single drill. Common checks are `kubectl rollout status`, `kubectl get endpoints`, `kubectl describe`, `kubectl logs`, and `kubectl exec`.
- Validate the requested behavior, not only that Kubernetes accepts the resource. For troubleshooting, inspect evidence in this order: `get`, `describe`, `logs`, then `exec`.

## Content Architecture

- `drills/` contains zero-hint, domain-organized practice prompts. `drills/README.md` is the canonical catalog and progression order.
- `answer-keys/` contains the reference solution and validation steps for the same stable drill ID. Treat an existing answer key as ground truth.
- `reference/` supplies command recall (`kubectl.md`), manifest shapes and validation (`manifests.md`), and repair mental models (`patterns.md`) used after repeated misses.
- `sessions/template.md` defines the dated session records under `sessions/`; preserve the template unchanged.
- `.github/skills/ckad-drilling-coach/SKILL.md` routes structured study requests to `COPILOT_SPACE_INSTRUCTIONS.md`, which is authoritative for coaching modes, corrections, topic order, and repetition limits.

## Repository Conventions

- Add drills in matched pairs: a zero-hint prompt in the relevant `drills/` file and its complete solution plus verification in the matching `answer-keys/` file. Add the stable domain-prefixed ID to the drill catalog.
- Each prompt states difficulty, target time, scenario, expected outcome, and common traps. Give required information in the scenario; raise difficulty by combining known concepts rather than withholding requirements.
- Keep answer keys practical and concise. Accept functionally equivalent Kubernetes alternatives, but explain material tradeoffs and provide the minimal correction for an invalid attempt.
- For a CKAD coaching session, start from the planned drill and current session state—never a random warm-up. Give one zero-hint scenario, wait for the full attempt, then review it using: verdict, what worked, exact issue, why it matters, minimal correction, verification, and retention cue.
- After three clean repetitions, stop; after the same miss occurs three times, use `reference/patterns.md` to rebuild the mental model before drilling again. Record outcomes in a dated copy of the session template.
