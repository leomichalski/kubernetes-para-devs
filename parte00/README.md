# Arquitetura

![diagrama](../assets/kubernetes-cluster-architecture.svg)

Mais em <https://kubernetes.io/docs/concepts/architecture/>

## Detalhes sobre cada Componente

Mais em <https://kubernetes.io/pt-br/docs/concepts/overview/components/>

### Componentes Específicos do Control Plane

Cada nó do cluster (Node) pode desempenhar um ou mais papéis diferentes. Caso um Node rode algum componente do Control Plane, ele é considerado parte do Control Plane.

#### kube-apiserver

O "API Server" expõe endpoints HTTP usados para comunicação de usuários (sysadmins) com o cluster e para comunicação entre os componentes do cluster.

Mais em <https://kubernetes.io/docs/concepts/overview/kubernetes-api/>

#### etcd

Armazenamento usado pela API do cluster para persistir dados.

#### kube-scheduler

Observa os Pods recém-criados e que ainda não foram atribuídos a um nó, e seleciona um nó para executá-los.

#### kube-controller-manager

Componente da camada de gerenciamento que executa os processos de controlador.

Mais na [Parte 7](../parte07) da aula.

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
