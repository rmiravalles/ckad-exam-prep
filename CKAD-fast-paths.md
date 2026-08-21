# CKAD Fast Paths

Generate a base object quickly, then edit only the fields the scenario requires. Always inspect generated YAML before applying it.

## Pod

```sh
kubectl run NAME --image=IMAGE --restart=Never --dry-run=client -o yaml > pod.yaml
```

Common edits: `command`, `args`, `env`, `ports`, `volumeMounts`, `volumes`, and probes.

## Deployment

```sh
kubectl create deployment NAME --image=IMAGE --dry-run=client -o yaml > deployment.yaml
```

Common edits: `replicas`, labels and selector, container port, configuration injection, and probes.

## Service

```sh
kubectl expose deployment NAME --port=80 --target-port=8080 --type=ClusterIP --dry-run=client -o yaml > service.yaml
```

Immediately verify the selector against the Deployment Pod-template labels.

## ConfigMap and Secret

```sh
kubectl create configmap NAME --from-literal=KEY=VALUE --dry-run=client -o yaml > configmap.yaml
kubectl create secret generic NAME --from-literal=KEY=VALUE --dry-run=client -o yaml > secret.yaml
```

Common edits: add more keys, then reference the exact name and key from `env`, `envFrom`, or a volume.

## Job and CronJob

```sh
kubectl create job NAME --image=busybox --dry-run=client -o yaml > job.yaml
kubectl create cronjob NAME --image=busybox --schedule='*/5 * * * *' --dry-run=client -o yaml > cronjob.yaml
```

For Job templates, set a valid `restartPolicy` and provide the intended command.

## Explain before guessing

```sh
kubectl explain pod.spec.containers.livenessProbe
kubectl explain deployment.spec.template.spec --recursive
```

Use `kubectl explain` when you know the resource shape but not the exact field hierarchy.