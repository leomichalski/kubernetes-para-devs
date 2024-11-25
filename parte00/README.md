# Visão geral de um Cluster Kubernetes

## O que é um cluster?

Um cluster Kubernetes (k8s), basicamente, é um conjunto de nós. Ele tem um nó central, chamado de `Control plane` e nós secundários, chamados de `nodes` ou `worker nodes`. O diagrama abaixo é uma representação em alto nível de um cluster. 

![Diagrama básico de um cluster](../assets/cluster_basico.svg)

O Control Plane controla todos os outros nós. Ele pode criar novos nós, e mantém o estado da aplicação.
Os worker nodes são os nós que contém os containers de uma aplicação.

## Arquitetura de um cluster

No diagrama abaixo, temos uma arquitetura mais detalhada de um cluster.

![Diagrama detalhado de um cluster](../assets/kubernetes-cluster-architecture.svg)

Mais em <https://kubernetes.io/docs/concepts/architecture/>

## O que têm em um Control Plane?

Com base no [diagrama acima](../assets/kubernetes-cluster-architecture.svg), temos os seguintes componentes em um Control Plane:

- [`kube-api-server`](https://kubernetes.io/docs/concepts/overview/kubernetes-api/): é uma API RESTful que expõe endpoints HTTP. É por meio dela que um usuário do k8s pode se comunicar com o Control Plane. A ferramenta de linha de comando [`kubectl`](https://kubernetes.io/docs/reference/kubectl/) é o cliente padrão desse servidor. No entanto, ela não é a única forma de se comunicar com a API (o comando [`kubeadm`](https://kubernetes.io/docs/reference/setup-tools/kubeadm/) também faz essa comunicação, por exemplo).
- [`etcd`](https://github.com/etcd-io/etcd): é um banco de dados open source utilizado pelo Control Plane para persistir os dados do cluster.
- [`kube-scheduler`](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-scheduler/): é um processo do Control Plane que define para qual Worker Node um Pod vai.
- [`kube-controller-manager`](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-controller-manager/): é um componente (daemon) que executa processos de controle do cluster. Ele conversa com o `kube-api-server` para verificar o estado do cluster e, com base nesse estado, executa processos de controle.

## O que têm em um Worker Node?

### Detalhes sobre cada Componente

Mais em <https://kubernetes.io/pt-br/docs/concepts/overview/components/>

### Componentes Específicos do Control Plane

Cada nó do cluster (Node) pode desempenhar um ou mais papéis diferentes. Caso um Node rode algum componente do Control Plane, ele é considerado parte do Control Plane.

#### kube-cloud-controller-manager (opcional)

O conceito do Cloud Controller Manager (CCM) foi originalmente criado para permitir que o código específico de provedor de nuvem e o núcleo do Kubernetes evoluíssem independentemente um do outro. O Cloud Controller Manager é executado junto com outros componentes principais, como o Kubernetes controller manager, o servidor de API e o scheduler. Também pode ser iniciado como um addon do Kubernetes, caso em que é executado em cima do Kubernetes.

### Componentes de Todos os Nodes

Os seguintes componentes são executados em cada um dos nós do cluster.

#### kubelet

Garante que os contêineres estejam sendo executados em um Pod. O kubelet não gerencia contêineres que não foram criados pelo Kubernetes.

#### kube-proxy

Mantém regras de rede nos nós. Estas regras de rede permitem a comunicação de rede com seus pods a partir de sessões de rede dentro ou fora de seu cluster.

kube-proxy usa a camada de filtragem de pacotes do sistema operacional se houver uma e estiver disponível (como iptables ou ebpf). Caso contrário, o kube-proxy encaminha o tráfego ele mesmo.

#### Container Runtime Interface (CRI)

O CRI é um "plugin interface" que permite ao kubelet usar diversos "container runtimes" diferentes, sem precisar recompilar componentes do cluster.

"Container runtime" é o software responsável por rodar containers. Exemplos: Docker, containerd, CRI-O e Podman.

### Addons

#### DNS

Embora os outros complementos não sejam estritamente necessários, todos os clusters do Kubernetes devem ter um DNS do cluster, já que muitos exemplos dependem disso.

O DNS do cluster é um servidor DNS, além de outros servidores DNS em seu ambiente, que fornece registros DNS para serviços do Kubernetes.

Os contêineres iniciados pelo Kubernetes incluem automaticamente esse servidor DNS em suas pesquisas DNS.
