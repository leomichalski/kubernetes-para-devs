# Service

Pode se referir a vários Deployments diferentes. Serve para fazer o balanceamento de carga entre os pods do Deployment.

Mais em: <https://kubernetes.io/docs/concepts/services-networking/service/>

## Ver Services existentes

```bash
kubectl get deployments --namespace default --kubeconfig kubeconfig
```

## Criar recursos

```bash
kubectl apply -f parte03 --namespace default --kubeconfig kubeconfig
```

## Testar acesso ao Django

Fazer "port forwarding" para ver se o Django está funcionando. Port forwarding é ótimo para debugar aplicações.

```bash
kubectl port-forward service/exemplo 8000:8000 --namespace default --kubeconfig kubeconfig
```

Acessar Django em <http://localhost:8000>

Observe que, usando Services, diferente da parte02, já não há necessidade de saber informações a respeito de Pods específicos!

## Diferenças para a parte02

```diff
diff --color -r '--exclude=README.md' parte02/django-deployment.yaml parte03/django-deployment.yaml
30c30
<           value: postgres://postgres:postgres@10-244-0-54.default.pod.cluster.local:5432/postgres
---
>           value: postgres://postgres:postgres@exemplo-postgres.default.svc.cluster.local:5432/postgres
Only in parte03: django-service.yaml
Only in parte03: postgres-service.yaml
```

Comando usado:

```bash
diff -r parte02 parte03 --exclude=README.md
```
