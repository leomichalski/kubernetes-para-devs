# Service

Pode se referir a vários Deployments diferentes. Serve para fazer o balanceamento de carga entre os pods do Deployment.

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
