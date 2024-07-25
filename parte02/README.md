# Deployment

É uma forma de se fazer um conjunto de Pods. Outra possibilidade é usar recursos de tipo DaemonSet ou StatefulSet. A diferença entre um Deployment e um DaemonSet é que o DaemonSet roda um pod em cada nó do cluster. A diferença entre um Deployment e um StatefulSet é que o StatefulSet dá um número para cada pod, mantendo separadamente o estado de cada um deles (como volumes etc).

Mais em: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

## Ver Deployments existentes no namespace "default"

```bash
kubectl get deployments --namespace default --kubeconfig kubeconfig
```

## Criar o Deployment do postgres

```bash
kubectl apply -f parte02/postgres-deployment.yaml --namespace default --kubeconfig kubeconfig
```

## Conferir IP do único Pod do Deployment do postgres

```bash
kubectl get pods -o wide --namespace default --kubeconfig kubeconfig
```

Na linha 25 do arquivo `django-deployment.yaml`, usando qualquer editor de texto, substituir "10-244-0-54" pelo IP do Pod. Atenção: use hifens (10-244-0-54) no lugar dos pontos (10.244.0.54).

```bash
vim parte02/django-deployment.yaml
```

## Criar o Deployment do Django

```bash
kubectl apply -f parte02/django-deployment.yaml --namespace default --kubeconfig kubeconfig
```

## Testar acesso ao Django

Fazer "port forwarding" para ver se o Django está funcionando. Port forwarding é ótimo para debugar aplicações.

```bash
kubectl port-forward deployment/exemplo 8000:8000 --namespace default --kubeconfig kubeconfig
```

Acessar Django em <http://localhost:8000>

## Ver histórico de mudanças do Deployment do Django

```bash
kubectl rollout history deployment/exemplo --namespace default --kubeconfig kubeconfig
```

Obs: Há formas mais fáceis de especificar o kubeconfig e o namespace, porém não é o foco dessa aula.
