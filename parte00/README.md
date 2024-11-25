# Visão geral de um Cluster Kubernetes

## O que é um cluster?

Um cluster Kubernetes (k8s), basicamente, é um conjunto de nós. Ele tem um nó central, chamado de `Control plane` e nós secundários, chamados de `nodes` ou `worker nodes`. O diagrama abaixo é uma representação em alto nível de um cluster. 

![Diagrama básico de um cluster](../assets/cluster_basico.svg)

O Control Plane controla todos os outros nós. Ele pode criar novos nós, e mantém o estado da aplicação.
Os worker nodes são os nós que contém os containers de uma aplicação.

## Arquitetura de um cluster

No diagrama abaixo, temos uma arquitetura mais detalhada de um cluster.

![Diagrama detalhado de um cluster](../assets/kubernetes-cluster-architecture.svg)

## O que têm em um Control Plane?

Com base no [diagrama acima](../assets/kubernetes-cluster-architecture.svg), temos os seguintes componentes em um Control Plane:

- [`kube-api-server`](https://kubernetes.io/docs/concepts/overview/kubernetes-api/): é uma API RESTful que expõe endpoints HTTP. É por meio dela que um usuário do k8s pode se comunicar com o Control Plane. A ferramenta de linha de comando [`kubectl`](https://kubernetes.io/docs/reference/kubectl/) é o cliente padrão desse servidor. No entanto, ela não é a única forma de se comunicar com a API (o comando [`kubeadm`](https://kubernetes.io/docs/reference/setup-tools/kubeadm/) também faz essa comunicação, por exemplo).
- [`etcd`](https://github.com/etcd-io/etcd): é um banco de dados open source utilizado pelo Control Plane para persistir os dados do cluster.
- [`kube-scheduler`](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-scheduler/): é um processo do Control Plane que define para qual Worker Node um Pod vai.
- [`kube-controller-manager`](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-controller-manager/): é um componente (daemon) que executa processos de controle do cluster. Ele conversa com o `kube-api-server` para verificar o estado do cluster e, com base nesse estado, executa processos de controle.
- [`kube-cloud-controller-manager`](https://kubernetes.io/docs/concepts/architecture/cloud-controller/): a ideia desse componente é a de realizar a integração de um cluster com a API de um provedor de cloud, separando os componentes que interagem com a cloud com os que interagem somente com o cluster. 

## O que têm em um Worker Node?

- [`kubelet`](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/): é um processo que recebe e executa comandos do Control Plane, servindo como um "gerenciador" dos Pods de um Node. Ele garante que o node e os containers estão saudáveis por meio de healthchecks, entre outras funções.
- [`kube-proxy`](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-proxy/): é um [proxy de rede](https://en.wikipedia.org/wiki/Proxy_server) interno. Ele garante que requisições a um Service sejam direcionadas ao Pod correto por trás do Service. Caso um service tenha muitos Pods, ele também pode realizar [load balancing](https://en.wikipedia.org/wiki/Load_balancing_(computing)).
- [`CRI(Container Runtime Interface)`](https://kubernetes.io/docs/concepts/architecture/cri/): permite que o Worker Node execute diferentes tipos de runtimes de containers (por exemplo: Docker, containerd...). O `kubelet` utiliza runtimes de containers para realizar o gerenciamento dos Pods. A CRI, portanto, é o protocolo de comunicação entre o `kubelet` e o runtime do container.

## Addons

### DNS

Embora os outros complementos não sejam estritamente necessários, todos os clusters do Kubernetes devem ter um DNS do cluster, já que muitos exemplos dependem disso.

O DNS do cluster é um servidor DNS, além de outros servidores DNS em seu ambiente, que fornece registros DNS para serviços do Kubernetes.

Os contêineres iniciados pelo Kubernetes incluem automaticamente esse servidor DNS em suas pesquisas DNS.
