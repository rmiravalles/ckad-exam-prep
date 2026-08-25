# CKAD Exam Prep

Hands-on Kubernetes Certified Application Developer practice built around short, repeatable drills. Attempt a realistic scenario from memory, review it against a trusted answer key, correct the underlying pattern, and repeat with fresh values.

This is a study system, not a substitute for the official CKAD curriculum or Kubernetes documentation. Use it with a Kubernetes environment where you can create, inspect, and troubleshoot resources.

## Start drilling

1. Open [the drill index](drills/README.md) and choose the next scenario.
2. Attempt the prompt without hints in a disposable namespace or cluster.
3. Review only afterward in the corresponding file under [answer-keys/](answer-keys/).
4. Use [reference material](reference/) to repair a missed concept or verify a command.
5. Record a session using [the session template](sessions/template.md), then schedule a fresh repetition.

Stop after three clean repetitions. If the same mistake occurs three times, pause and rebuild the mental model before resuming.

## 🤖 Using the Copilot skill

This repository includes the [CKAD Drilling Coach skill](.github/skills/ckad-drilling-coach/SKILL.md), which turns the study materials into structured Copilot-led sessions.

In VS Code Copilot Chat, invoke it directly with `/ckad-drilling-coach`, followed by a session goal, topic, or weak area. For example:

```text
/ckad-drilling-coach Start a cold-recall session on ConfigMaps and Secrets.
```

```text
/ckad-drilling-coach Review my recent mistake patterns and plan the next session.
```

```text
/ckad-drilling-coach Run a timed mixed drill for Pods, Services, and probes.
```

Copilot can also load the skill automatically when you ask to start a CKAD drill, practice Kubernetes manifests, review a session, plan CKAD study, record mistakes, or prepare for the exam. The skill reads the existing instructions and templates, establishes the session state, gives one zero-hint scenario at a time, verifies answers against trusted references, and records the session outcome.

## Repository layout

| Location | Purpose |
| --- | --- |
| [drills/](drills/) | Zero-hint scenarios organized by domain. Start with [the drill index](drills/README.md). |
| [answer-keys/](answer-keys/) | Matching reference solutions and validation steps. |
| [reference/](reference/) | Command recall, manifest examples, validation checks, mental models, and recurring repair drills. |
| [sessions/](sessions/) | Reusable regular and timed-session template plus your dated session records. |
| [COPILOT_SPACE_INSTRUCTIONS.md](COPILOT_SPACE_INSTRUCTIONS.md) | The coaching contract used by the Copilot skill. |
| [.github/skills/ckad-drilling-coach/SKILL.md](.github/skills/ckad-drilling-coach/SKILL.md) | Copilot skill for running and reviewing structured study sessions. |

## Sources

- [CKAD certification overview](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/)
- [Kubernetes documentation](https://kubernetes.io/docs/)
- [Kubernetes API reference](https://kubernetes.io/docs/reference/kubernetes-api/)
- [kubectl reference](https://kubernetes.io/docs/reference/kubectl/)
- [Kubernetes task guides](https://kubernetes.io/docs/tasks/)

## ✅ Recommended habits

- Practice from memory first; use references to correct work, not to replace recall.
- Validate manifests with `kubectl apply`, `kubectl get`, `kubectl describe`, and logs in a disposable practice namespace or cluster.
- Prefer `kubectl ... --dry-run=client -o yaml` to create a starting point under time pressure, then edit only the fields the scenario requires.
- Track repeated errors. A syntax fix is not enough when the underlying behavior is unclear.
- Shift to mixed and timed drills only after individual topics are reliable.
- In the final one to two days before the exam, prioritize accuracy, confidence, and known weak spots over new material.