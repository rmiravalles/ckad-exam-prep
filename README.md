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

This repository includes the [CKAD Drilling Coach skill](.github/skills/ckad-drilling-coach/SKILL.md), which turns the study materials into structured Copilot-led sessions. For deliberate practice, invoke it explicitly in VS Code Copilot Chat:

```text
/ckad-drilling-coach MODE, TOPIC OR DRILL ID, TIME AVAILABLE, WEAK AREA, CORRECTION DEPTH
```

Name the mode, a topic or drill ID from [the drill catalog](drills/README.md#drill-catalog), available time, and a known weak area when you have them. This lets the coach select the right scenario and feedback depth without a generic warm-up.

| Mode | Use it when | Coach behavior |
| --- | --- | --- |
| `Cold recall` | You know the topic and want to test recall. | Gives one zero-hint scenario and waits for a complete answer. |
| `Line-by-line` | The topic is new or unstable. | Explains each relevant field, why it exists, and what breaks when it is wrong. |
| `Exam` | You are doing timed or final-review practice. | Keeps corrections concise and focuses on the minimal repair and verification. |

### Effective prompts

Start a focused cold-recall session:

```text
/ckad-drilling-coach Cold recall, C-02, 15 minutes. I confuse Secret volume items and paths. Use descriptive corrections.
```

Learn a topic before returning to recall:

```text
/ckad-drilling-coach Teach W-03 line by line. I understand Deployments but not Kustomize overlays.
```

Run a short timed review:

```text
/ckad-drilling-coach Run an exam-mode review of T-02 and T-03. I have 15 minutes; keep corrections concise.
```

Review an existing attempt rather than start a new drill:

```text
/ckad-drilling-coach Review my attempt for SS-02. Classify each issue, explain the Kubernetes behavior, show the minimal correction, and give me a verification command.
```

After an attempted drill, the coach reports what worked, the exact issue, why Kubernetes behaves that way, the minimal repair, an exact verification command, and a reusable retention cue. It distinguishes invalid work from valid alternatives and does not reveal a complete answer before an attempt.

At the end of a session, ask the coach to create or update a dated record under [sessions/](sessions/) from [the session template](sessions/template.md). Record recurring mistakes, verification evidence, and the next drill ID so the next session starts from evidence rather than a random prompt.

Copilot can load the skill automatically when you ask to start a CKAD drill, practice Kubernetes manifests, review a session, plan CKAD study, record mistakes, or prepare for the exam. Explicit invocation is preferable for a structured session because it makes the mode, scope, time limit, and correction depth clear.

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