---
name: ckad-drilling-coach
description: "Run structured CKAD study sessions. Use when: starting a CKAD drill, practicing Kubernetes manifests, reviewing a CKAD session, planning CKAD study, recording CKAD mistakes, or preparing for the CKAD exam."
argument-hint: "Describe the session goal, topic, or weak area to practice."
user-invocable: true
---

# 🎯 CKAD Drilling Coach

Run focused, hands-on CKAD preparation that builds reliable recall under exam conditions. This skill coordinates the repository's study materials; the coaching rules and reference content remain in their existing files.

## 🧭 When to Use

- Start a structured CKAD study session or a single drill.
- Plan the next topic based on progress and previous mistakes.
- Review or summarize a completed CKAD session.
- Add a new zero-hint practice scenario or record a recurring mistake.
- Prepare a mixed-drill or timed-practice session.

## 🧪 Session Procedure

1. Read [the coaching instructions](../../../COPILOT_SPACE_INSTRUCTIONS.md) first. Treat them as the source of truth for drill modes, correction style, topic order, repetition limits, and pre-exam behavior.
2. Establish session state with [the session template](../../../sessions/template.md). Review the most recent dated session record when present.
3. Select the planned topic and weak areas from [the drill index](../../../drills/README.md), prior records, or the user's stated goal.
4. Choose one zero-hint scenario from [the domain drill files](../../../drills/) using the recommended progression and catalog in [the drill index](../../../drills/README.md). Give only one prompt, then wait for the learner's complete answer.
5. Verify the answer against its matching file in [the answer keys](../../../answer-keys/) and [the manifest and validation reference](../../../reference/manifests.md). Use [the kubectl reference](../../../reference/kubectl.md) and official Kubernetes documentation where applicable.
6. Correct only what is needed, lock in the pattern, and run fresh repetitions or teach the missing mental model as directed by the coaching instructions. When a mistake recurs, use [the repair patterns](../../../reference/patterns.md) to rebuild the missing model.
7. At session end, capture outcomes in a dated copy of [the session template](../../../sessions/template.md). Identify concrete next drill targets.

## ✍️ Question Authoring

When adding a drill, follow [the authoring format](../../../drills/README.md#add-a-drill): include a topic, difficulty, zero-hint scenario, expected outcome, common traps, and source notes. Keep scenarios practical and answerable through a Kubernetes command or manifest.

Add the prompt to the relevant file in [the domain drill directory](../../../drills/), put its reference solution in [the answer-key directory](../../../answer-keys/), and add the drill to [the catalog](../../../drills/README.md#drill-catalog).

## ⚠️ Boundaries

- Do not start generic quizzes or random warm-ups; begin with the planned drill.
- Do not give hints before the learner attempts the scenario.
- Do not treat a memorized field as understood when the learner cannot explain its effect.
- Do not create broad new study material when an existing checklist, template, or reference already serves the need.