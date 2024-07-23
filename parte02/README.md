# Deployment e HPA

## Deployment

É uma forma de se fazer um conjunto de Pods. Outra possibilidade é usar recursos de tipo DaemonSet ou StatefulSet. A diferença entre um Deployment e um DaemonSet é que o DaemonSet roda um pod em cada nó do cluster. A diferença entre um Deployment e um StatefulSet é que o StatefulSet dá um número para cada pod, mantendo separadamente o estado de cada um deles (como volumes etc).

## Horizontal Pod Autoscaler (HPA)

É usado para controlar a quantidade de Pods que há em um Deployment. Por exemplo, se o uso de CPU estiver muito alto, o HPA aumentaria a quantidade de pods. Também é possível utilizar o Vertical Pod Autoscaler (VPA), que aumentaria a quantidade de recursos de cada pod em vez de aumentar a quantidade de Pod.
