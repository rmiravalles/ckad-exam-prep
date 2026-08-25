# kubectl Reference

Generate a base object quickly, inspect the generated YAML, and edit only the fields the scenario requires.

## Fast creation

```sh
kubectl create deployment NAME --image=IMAGE --dry-run=client -o yaml
kubectl run NAME --image=IMAGE --restart=Never --dry-run=client -o yaml
kubectl create job NAME --image=IMAGE --dry-run=client -o yaml
kubectl create cronjob NAME --image=IMAGE --schedule='*/5 * * * *' --dry-run=client -o yaml
kubectl create configmap NAME --from-literal=KEY=VALUE --dry-run=client -o yaml
kubectl create secret generic NAME --from-literal=KEY=VALUE --dry-run=client -o yaml
kubectl expose deployment NAME --port=80 --target-port=8080 --type=ClusterIP --dry-run=client -o yaml
```

## Common edits

| Object | Fields to check |
| --- | --- |
| Pod | `command`, `args`, `env`, `ports`, `volumeMounts`, `volumes`, probes |
| Deployment | `replicas`, labels, selector, container port, configuration injection, probes |
| Service | Selector matches Pod-template labels; `targetPort` matches the listening port |
| ConfigMap or Secret | Exact names and keys used by `env`, `envFrom`, or volumes |
| Job or CronJob | Command and `restartPolicy`; Job templates use `Never` or `OnFailure` |

## Inspect and debug

```sh
kubectl get pods
kubectl get deploy
kubectl get svc
kubectl get cm
kubectl get secret
kubectl get pv
kubectl get pvc
kubectl get all
kubectl describe pod POD
kubectl logs POD
kubectl exec -it POD -- sh
kubectl get pod POD -o yaml
kubectl get pod POD -o wide
kubectl get pod POD -o jsonpath='{...}'
kubectl logs POD -c CONTAINER
kubectl exec -it POD -c CONTAINER -- sh
```

Apply with `kubectl apply -f FILE.yaml`; use `kubectl edit`, `kubectl replace -f`, or `kubectl delete -f` only when the scenario calls for it. Start diagnosis with `get`, then `describe`, then `logs`, then `exec`.

## Explain before guessing

```sh
kubectl explain pod.spec.containers.livenessProbe
kubectl explain deployment.spec.template.spec --recursive
```

Use `kubectl explain` when you know the resource shape but need the exact field hierarchy.