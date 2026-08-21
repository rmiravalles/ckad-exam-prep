# CKAD Exam Prep

A focused workspace for building Kubernetes Certified Application Developer (CKAD) fluency through hands-on, memory-first practice. It is designed around short, repeatable drills: solve a realistic scenario with no hints, compare the result against a trusted reference, capture the correction, then repeat with fresh values until the pattern is reliable.

This repository is a study system, not a substitute for the official CKAD curriculum or Kubernetes documentation. Use it alongside a Kubernetes environment where you can create, inspect, and troubleshoot resources.

## Study approach

The intended loop is:

1. Choose the next topic and any weak areas from the topic checklist and prior session notes.
2. Start a session with the session-start checklist.
3. Attempt one scenario from memory, without hints.
4. Verify the manifest or command against an answer key, reference material, or the Kubernetes API.
5. Record meaningful mistakes and the corrected pattern.
6. Repeat the scenario with different names and values. Stop after three clean repetitions; if the same mistake persists, pause to rebuild the underlying concept before drilling again.
7. End by writing a concise session summary and setting the next drill targets.

The coach guidance in [COPILOT_SPACE_INSTRUCTIONS.md](COPILOT_SPACE_INSTRUCTIONS.md) defines the expected progression: mental model, syntax, drill, then timed repetition. It also gives the recommended topic order and rules for cold-recall, line-by-line, and pre-exam practice.

## Quick start

1. Read [CKAD-topic-checklist.md](CKAD-topic-checklist.md) and select one unchecked topic.
2. Copy the session templates when beginning a new session:
	- [CKAD-session-start-checklist.md](CKAD-session-start-checklist.md)
	- [CKAD-session-log-template.md](CKAD-session-log-template.md)
	- [CKAD-session-summary-template.md](CKAD-session-summary-template.md)
3. Start with a relevant prompt from [CKAD-first-10-drills.md](CKAD-first-10-drills.md), or add a scenario to [CKAD-question-bank-template.md](CKAD-question-bank-template.md).
4. Build and test your answer in a Kubernetes cluster. Use [kubectl-cheat-sheet.md](kubectl-cheat-sheet.md) to generate base manifests quickly and inspect results.
5. Compare your work with [CKAD-sample-manifests.md](CKAD-sample-manifests.md) where applicable, then log the correction and schedule a fresh repetition.

For a more structured flow, choose a prompt from [CKAD-drill-catalog.md](CKAD-drill-catalog.md), validate it with [CKAD-validation-checklist.md](CKAD-validation-checklist.md), and consult its answer key only after attempting the scenario.

## Using the Copilot skill

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

## Repository contents

| File | Purpose |
| --- | --- |
| [COPILOT_SPACE_INSTRUCTIONS.md](COPILOT_SPACE_INSTRUCTIONS.md) | Instructions for running disciplined CKAD coaching sessions, including drill modes and correction rules. |
| [CKAD-topic-checklist.md](CKAD-topic-checklist.md) | Tracks the CKAD topics to practice, from fundamentals through timed simulations. |
| [CKAD-session-start-checklist.md](CKAD-session-start-checklist.md) | Ensures each study session starts from prior context and a concrete plan. |
| [CKAD-session-log-template.md](CKAD-session-log-template.md) | Append-only record of mistakes, corrections, memory cues, and follow-up drills. |
| [CKAD-session-summary-template.md](CKAD-session-summary-template.md) | End-of-session review of practice, locked patterns, recurring mistakes, and next targets. |
| [CKAD-first-10-drills.md](CKAD-first-10-drills.md) | Starter scenarios covering common CKAD resource types and patterns. |
| [CKAD-question-bank-template.md](CKAD-question-bank-template.md) | Format for adding your own zero-hint scenarios with reference answers and common traps. |
| [CKAD-sample-manifests.md](CKAD-sample-manifests.md) | Reference YAML for common Pods, workloads, Services, configuration, probes, and storage. |
| [kubectl-cheat-sheet.md](kubectl-cheat-sheet.md) | Fast creation, inspection, debugging, and YAML-generation commands for practice. |
| [CKAD-drill-catalog.md](CKAD-drill-catalog.md) | Index of zero-hint drills, their difficulty, time budgets, prerequisites, and answer keys. |
| [drills/](drills/) | Domain-organized zero-hint drills, including fundamentals, configuration, workloads, networking, storage, troubleshooting, and timed simulations. |
| [answer-keys/](answer-keys/) | Reference solutions and validation steps, separated from prompts to preserve recall practice. |
| [CKAD-validation-checklist.md](CKAD-validation-checklist.md) | Resource-specific checks for verifying intended Kubernetes behavior. |
| [CKAD-mistake-patterns.md](CKAD-mistake-patterns.md) | Curated recurring mistakes, mental models, corrections, and repair drills. |
| [CKAD-timed-simulation-template.md](CKAD-timed-simulation-template.md) | Template for planning, running, and reviewing timed mixed drills. |
| [CKAD-fast-paths.md](CKAD-fast-paths.md) | Fast `kubectl` generation patterns and high-frequency edits. |
| [CKAD-concept-maps.md](CKAD-concept-maps.md) | Compact mental models for common conceptual failure points. |
| [sources.md](sources.md) | Official and local sources for verifying drills and answer keys. |
| [.github/skills/ckad-drilling-coach/SKILL.md](.github/skills/ckad-drilling-coach/SKILL.md) | Copilot skill for running and reviewing structured CKAD study sessions. |

## Recommended habits

- Practice from memory first; use references to correct work, not to replace recall.
- Validate manifests with `kubectl apply`, `kubectl get`, `kubectl describe`, and logs in a disposable practice namespace or cluster.
- Prefer `kubectl ... --dry-run=client -o yaml` to create a starting point under time pressure, then edit only the fields the scenario requires.
- Track repeated errors. A syntax fix is not enough when the underlying behavior is unclear.
- Shift to mixed and timed drills only after individual topics are reliable.
- In the final one to two days before the exam, prioritize accuracy, confidence, and known weak spots over new material.