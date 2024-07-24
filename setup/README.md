# Setup

> [!IMPORTANT]  
> Em caso de dificuldade com o setup, basta levantar uma mão e pedir ajuda!

> [!NOTE]
> O foco não é explicar cada comando usado no setup.

Há vários detalhes no setup, demoraria muito tempo para explicar tudo. A ideia é que todo mundo consiga fazer o setup funcionar para poder usar o Kubernetes. Em empresas grandes, provavelmente, o cluster de desenvolvimento já teria sido configurado pela pessoa que cuida da infraestrutura, não pela pessoa desenvolvedora de software.

## Instalar Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# testar
sudo docker version
```

## Instalar Kind (Kubernetes In Docker)

Para Linux AMD64 / x86_64

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

# testar
kind --version
```

Mais opções de instalação em <https://kind.sigs.k8s.io/docs/user/quick-start/#installation>

## Instalar kubectl

Para Linux AMD64 / x86_64

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

# testar
kubectl version
```

Mais opções de instalação em <https://kubernetes.io/docs/tasks/tools/#kubectl>

## Instalar Helm3

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
sh ./get_helm.sh

# testar
helm version
```

Mais opções de instalação em <https://helm.sh/docs/intro/install/>

## Configuração do Kind

### Clonar este repositório

```bash
git clone https://github.com/leomichalski/kubernetes-for-devs.git
```

### Navegar até a pasta principal do repositório

```bash
cd kubernetes-for-devs
```

### Começar cluster Kubernetes com Kind

```bash
kind create cluster --config setup/kind_config.yaml
```

### Salver arquivo kubeconfig para poder usar o kubectl

```bash
kind get kubeconfig --name aula-gces | tee kubeconfig
```

### Testar kubectl

Sempre usar a flag "--kubeconfig kubeconfig" quando for usar o kubectl. Há outras formas de facilitar o uso do kubectl, porém não é o foco dessa aula.

```bash
kubectl get nodes --kubeconfig kubeconfig
```

### Instalar ingress-nginx

Necessário para a parte05.

```bash
# Criar namespace para instalar o ingress-nginx
kubectl create namespace ingress-nginx --kubeconfig kubeconfig

# Setup do ingress-nginx no Kind (sem Helm, assunto de outra parte)
kubectl apply --namespace ingress-nginx -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml --kubeconfig kubeconfig
```

### Instalar cert-manager

Necessário para a parte06.

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.15.1/cert-manager.yaml
```

## Referências

* Instalação das ferramentas essenciais. Link: <https://github.com/arthurbdiniz/kind-tutorial/blob/master/0-install-tools.sh>. Autor: Arthur Diniz.
* How to Test Ingress in a kind cluster. Link: <https://dustinspecker.com/posts/test-ingress-in-kind/>. Autor: Dustin Specker.
