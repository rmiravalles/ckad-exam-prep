# 🔁 Workload Drills

## 🧪 W-01: Deployment with container port

- **Difficulty:** Core
- **Target time:** 6 minutes
- **Scenario:** Create a Deployment named `web` with three replicas. Each Pod must run `nginx:1.27`, expose container port `8080`, and carry the label `app=web`.
- **Expected outcome:** The Deployment has three available replicas and its selector matches the Pod-template labels.
- **Common traps:** Selector and template-label mismatch; putting `ports` at the Pod level; omitting `replicas`.

## 🧪 W-02: Rolling update and rollback

- **Difficulty:** Core
- **Target time:** 8 minutes
- **Scenario:** Create a Deployment named `api` with two replicas of `nginx:1.26`. Update it to `nginx:1.27`, confirm the rollout completes, then roll back to the previous revision.
- **Expected outcome:** The Deployment finishes both operations with two available replicas, and its final Pod template uses `nginx:1.26`.
- **Common traps:** Editing Pods instead of the Deployment; skipping rollout status; assuming an image update is complete before the new ReplicaSet is available.

## 🧪 W-03: Kustomize overlay

- **Difficulty:** Core
- **Target time:** 10 minutes
- **Scenario:** In an empty directory, create a Kustomize base for a Deployment named `catalog` with one `nginx:1.27` replica. Create an overlay that adds the `environment=staging` label and changes the replica count to three. Apply the overlay.
- **Expected outcome:** The resulting Deployment has three replicas and the label is present on the Deployment and Pod template.
- **Common traps:** Applying the base instead of the overlay; changing selector labels; placing `replicas` in the base when the overlay is required to own it.

## 🧪 W-04: Deploy an existing Helm chart

- **Difficulty:** Core
- **Target time:** 8 minutes
- **Scenario:** Add the Bitnami chart repository, then install the `bitnami/nginx` chart as release `edge` in namespace `edge-demo`, creating the namespace if needed. Configure the chart with two replicas and wait for the release to become ready.
- **Expected outcome:** `helm status edge -n edge-demo` reports a deployed release, and a two-replica workload is ready.
- **Common traps:** Forgetting `helm repo update`; omitting the namespace creation flag; validating only that Helm accepted the command rather than that workload resources are ready.