# Introdução a Kubernetes para Devs

## Organização

./kubernetes-for-devs
 * [parte00](./parte00): Arquitetura.
 * [parte01](./parte01): Pod.
 * [parte02](./parte02): Deployment e HPA.
 * [parte03](./parte03): Service.
 * [parte04](./parte04): Ingress.
 * [parte05](./parte05): Issuer.
 * [parte06](./parte06): Controller Pattern.

## Setup

Baseado em https://github.com/arthurbdiniz/kind-tutorial/blob/master/0-install-tools.sh

### Instalar Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
sudo docker version
```

### Instalar Kind (Kubernetes In Docker)

Para Linux AMD64 / x86_64

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
kind --version
```

Mais opções de instalação em <https://kind.sigs.k8s.io/docs/user/quick-start/#installation>

### Instalar kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version
```

Mais opções de instalação em <https://kubernetes.io/docs/tasks/tools/#kubectl>

## Configuração

### Começar cluster Kubernetes com Kind

```bash
kind create cluster --name aula-gces
```

### Salver arquivo kubeconfig para poder usar o kubectl

```bash
kind get kubeconfig --name aula-gces | tee kubeconfig
```

### Usar kubectl

Sempre usar a flag "--kubeconfig kubeconfig" quando for usar o kubectl.

```bash
kubectl get pods --kubeconfig kubeconfig
```

Há outras formas de facilitar o uso do kubectl, porém não é o foco dessa aula.
