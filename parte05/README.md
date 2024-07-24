# Ingress

Pode se referir a vários Services. Serve para atribuir um DNS (como google.com), que pode ser usado para acessar a aplicação que estiver rodando em determinados Deployments, DaemonSets ou StatefulSets.

## Setup do ingress-nginx

Coberto na seção de [setup](../setup). O foco desta parte não é aprender a instalar o `ingress-nginx`, é aprender a usar.

## Criar recursos

```bash
kubectl apply -f parte05 --namespace default --kubeconfig kubeconfig
```

## Ver Ingresses existentes

```bash
kubectl get ingress --namespace default --kubeconfig kubeconfig
```

## Apontar aula.gces.com para o IP do Kind

Caso isso fosse feito para o mundo todo, seria necessário possuir um registro DNS, um IP público e medidas de segurança. Porém, para fazer isso somente no seu computador, é possível editar o arquivo `/etc/hosts` do seu computador.

Em um comando só:

```bash
echo $(docker container inspect aula-gces-control-plane --format '{{ .NetworkSettings.Networks.kind.IPAddress }}') aula.gces.com | sudo tee -a /etc/hosts
```

Em dois comandos:

```bash
# Ver IP do container do Kind
docker container inspect aula-gces-control-plane --format '{{ .NetworkSettings.Networks.kind.IPAddress }}'

# Adicionar linha "SUBSTITUIR_POR_IP aula.gces.com" ao final do arquivo /etc/hosts
echo SUBSTITUIR_POR_IP aula.gces.com | sudo tee -a /etc/hosts
```

## Testar aula.gces.com

Acessar <http://aula.gces.com> em um browser para ver se funcionou.

## Deletar recursos

```bash
kubectl delete -f parte05 --namespace default --kubeconfig kubeconfig
```
