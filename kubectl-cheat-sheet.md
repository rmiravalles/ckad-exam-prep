# ⚡ kubectl Cheat Sheet for CKAD

## 🏗️ Fast creation
- Create from scratch with YAML output:
  - `kubectl create deployment NAME --image=IMAGE --dry-run=client -o yaml`
  - `kubectl run NAME --image=IMAGE --restart=Never --dry-run=client -o yaml`
  - `kubectl create job NAME --image=IMAGE --dry-run=client -o yaml`
  - `kubectl create cronjob NAME --image=IMAGE --schedule='*/5 * * * *' --dry-run=client -o yaml`
  - `kubectl create configmap NAME --from-literal=KEY=VALUE --dry-run=client -o yaml`
  - `kubectl create secret generic NAME --from-literal=KEY=VALUE --dry-run=client -o yaml`
  - `kubectl expose deployment NAME --port=80 --target-port=8080 --type=ClusterIP --dry-run=client -o yaml`

## 🔎 Inspect
- `kubectl get pods`
- `kubectl get deploy`
- `kubectl get svc`
- `kubectl get cm`
- `kubectl get secret`
- `kubectl get pv`
- `kubectl get pvc`
- `kubectl get all`
- `kubectl describe pod POD`
- `kubectl logs POD`
- `kubectl exec -it POD -- sh`

## ✏️ Apply and edit
- `kubectl apply -f FILE.yaml`
- `kubectl edit deployment NAME`
- `kubectl replace -f FILE.yaml`
- `kubectl delete -f FILE.yaml`

## 📤 Output
- `kubectl get pod POD -o yaml`
- `kubectl get pod POD -o wide`
- `kubectl get pod POD -o jsonpath='{...}'`

## 🩺 Debugging
- `kubectl explain PODSPEC_FIELD`
- `kubectl logs POD -c CONTAINER`
- `kubectl exec -it POD -c CONTAINER -- sh`
- `kubectl describe` before editing

## 🎯 CKAD habit
- Prefer `--dry-run=client -o yaml` to generate the base manifest, then edit only what is needed.
