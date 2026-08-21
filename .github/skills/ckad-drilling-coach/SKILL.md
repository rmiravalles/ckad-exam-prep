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
2. Establish session state with [the session-start checklist](../../../CKAD-session.md). Review the most recent session summary and session log when present.
3. Select the planned topic and weak areas from [the topic checklist](../../../CKAD-topic-checklist.md), [the drill catalog](../../../CKAD-drill-catalog.md), prior notes, or the user's stated goal.
4. Choose one zero-hint scenario from [the domain drill files](../../../drills/), [the starter drills](../../../CKAD-first-10-drills.md), or [the question bank](../../../CKAD-question-bank-template.md). Give only one prompt, then wait for the learner's complete answer.
5. Verify the answer against its matching file in [the answer keys](../../../answer-keys/) and [the validation checklist](../../../CKAD-validation-checklist.md). Use [sample manifests](../../../CKAD-sample-manifests.md), [the kubectl cheat sheet](../../../kubectl-cheat-sheet.md), and [the source list](../../../sources.md) where applicable.
6. Correct only what is needed, lock in the pattern, and run fresh repetitions or teach the missing mental model as directed by the coaching instructions. When a mistake recurs, use [the mistake patterns](../../../CKAD-mistake-patterns.md) and [the concept maps](../../../CKAD-concept-maps.md) to rebuild the missing model.
7. At session end, capture outcomes with [the session log](../../../CKAD-session.md) and [the session summary template](../../../CKAD-session.md). Identify concrete next drill targets.

## ✍️ Question Authoring

When adding a drill, follow [the question-bank template](../../../CKAD-question-bank-template.md): include a topic, difficulty, zero-hint scenario, expected outcome, reference answer, common traps, and source notes. Keep scenarios practical and answerable through a Kubernetes command or manifest.

Add the prompt to the relevant file in [the domain drill directory](../../../drills/), put its reference solution in [the answer-key directory](../../../answer-keys/), and add the drill to [the catalog](../../../CKAD-drill-catalog.md).

## ⚠️ Boundaries

- Do not start generic quizzes or random warm-ups; begin with the planned drill.
- Do not give hints before the learner attempts the scenario.
- Do not treat a memorized field as understood when the learner cannot explain its effect.
- Do not create broad new study material when an existing checklist, template, or reference already serves the need.