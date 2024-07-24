# HPA

## Horizontal Pod Autoscaler (HPA)

É usado para controlar a quantidade de Pods que há em um Deployment. Por exemplo, se o uso de CPU estiver muito alto, o HPA aumentaria a quantidade de pods. Também é possível utilizar o Vertical Pod Autoscaler (VPA), que aumentaria a quantidade de recursos de cada pod em vez de aumentar a quantidade de Pod.

## Ver HPAs existentes

```bash
kubectl get hpa --namespace default --kubeconfig kubeconfig
```

## Criar recursos

```bash
kubectl apply -f parte04 --namespace default --kubeconfig kubeconfig
```

## Deletar recursos

```bash
kubectl delete -f parte04 --namespace default --kubeconfig kubeconfig
```

## Diferenças para a parte03

```diff
diff --color -r '--exclude=README.md' parte03/django-deployment.yaml parte04/django-deployment.yaml
10d9
<   replicas: 3
35,41c34,40
<         # resources:
<         #   limits:
<         #     memory: 1.5Gi
<         #     cpu: "1"
<         #   requests:
<         #     memory: 1.5Gi
<         #     cpu: "1"
---
>         resources:
>           limits:
>             memory: 1.5Gi
>             cpu: "1"
>           requests:
>             memory: 1.5Gi
>             cpu: "1"
Only in parte04: django-hpa.yaml
```

Comando usado:

```bash
diff -r parte03 parte04 --exclude=README.md
```
