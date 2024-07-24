# Introdução a Kubernetes para Devs

## Organização

./kubernetes-para-devs
 * [setup](./setup): Setup das ferramentas necessárias para seguir o passo-a-passo.
 * [parte00](./parte00): Arquitetura.
 * [parte01](./parte01): Pod: um conjunto de containers.
 * [parte02](./parte02): Deployment: um tipo de conjunto de pods.
 * [parte03](./parte03): Service: faz o balanceamento de carga para os pods, pode se referir a diversos Deployments.
 * [parte04](./parte04): HPA: controla, automaticamente, a quantidade de Pods de um Deployment.
 * [parte05](./parte05): Ingress: em um cluster Kubernetes no qual todas as requisições chegam no mesmo IP e na mesma porta, os Ingresses são responsáveis por direcionar (de acordo com o DNS e o endpoint de cada requisição) essas requisições para os Services adequados. Também pode ser usado para outras finalidades.
 * [parte06](./parte06): Issuer: responsável por fornecer um certificado SSL para os Ingresses poderem criptografar (com HTTPS) as requisições que entram e saem.
 * [parte07](./parte07): Helm: uma forma de empacotar seus manifestos do Kubernetes.
