# HPA

## Horizontal Pod Autoscaler (HPA)

É usado para controlar a quantidade de Pods que há em um Deployment. Por exemplo, se o uso de CPU estiver muito alto, o HPA aumentaria a quantidade de pods. Também é possível utilizar o Vertical Pod Autoscaler (VPA), que aumentaria a quantidade de recursos de cada pod em vez de aumentar a quantidade de Pod.

## Ver HPAs existentes

```bash
kubectl get hpa --namespace default --kubeconfig kubeconfig
```

## Criar recursos

```bash
kubectl apply -f parte04 --namespace default --kubeconfig kubeconfig
```

## Deletar recursos

```bash
kubectl delete -f parte04 --namespace default --kubeconfig kubeconfig
```
