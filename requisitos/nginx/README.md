# Nginx

Usos do Nginx neste contexto.

## Load Balancer Externo

O seguinte Load Balancer pode ser um Nginx, um AWS ALB, um Azure Load Balancer ou outro Load Balancer.

```mermaid
graph LR
    subgraph Load Balancer
        A[Load Balancer]
    end
    subgraph Kubernetes Nodes
        B[Node 1]
        C[Node 2]
        D[Node 3]
    end
    A --> B
    A --> C
    A --> D
```

## `ingress-nginx`

Uso comum do `ingress-nginx` dentro de um cluster Kubernetes.

```mermaid
graph LR
    A[Ingress]

    subgraph Pods
        E[airflow-1]
        F[airflow-2]
        G[ej-admin-1]
        H[ej-api-1]
        I[ej-api-2]
        J[ej-api-3]
    end

     subgraph Services
        X[Service do Airflow]
        Y[Service do EJ Admin]
        Z[Service do EJ API]
    end
    
    A --Regra do airflow.lappis.rocks--> X
    A --Regra do ej-admin.lappis.rocks--> Y
    A --Regra do ej-api.lappis.rocks--> Z

    X[Service do Airflow] --> E
    X[Service do Airflow] --> F
    Y[Service do EJ ADMIN] --> G
    Z[Service do EJ API] --> H
    Z[Service do EJ API] --> I
    Z[Service do EJ API] --> J

```

