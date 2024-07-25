# Pod

É um conjunto de containers. É a unidade mais básica usada no caso de containers. Muitas vezes, há um container principal e os outros são chamados de "sidecars".

Mais em: https://kubernetes.io/docs/concepts/workloads/pods/

## Ver pods existentes no namespace "default"

```bash
kubectl get pods --namespace default --kubeconfig kubeconfig
```

## Criar o Pod definido no arquivo `pod.yaml`

```bash
kubectl apply -f parte01/pod.yaml --namespace default --kubeconfig kubeconfig
```

## Testar acesso ao Postgres

Fazer "port forwarding" para ver se o Postgres está funcionando. Port forwarding é ótimo para debugar aplicações.

```bash
kubectl port-forward pod/exemplo-postgres 5432:5432 --namespace default --kubeconfig kubeconfig
```

Acessar Postgres usando `psql` (também é possível usar `pgadmin`, `dbeaver` e outras ferramentas).

```bash
psql --host localhost --port 5432 --username postgres postgres
```

## Deletar o Pod criado anteriormente

```bash
kubectl delete pod/exemplo-postgres --namespace default --kubeconfig kubeconfig
```

Obs: Há formas mais fáceis de especificar o kubeconfig e o namespace, porém não é o foco dessa aula.
