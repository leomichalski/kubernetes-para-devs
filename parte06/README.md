# Issuer

Pode ser usado por vários recursos Ingress. É usado para se comunicar com uma autoridade certificadora para liberar um certificado SSL para o domínio escolhido. Dessa forma, é possível acessar a aplicação com HTTPS (em vez de somente HTTP). Por exemplo, <https://google.com> em vez de <http://google.com> .

## Instalar cert-manager (sem Helm)

Coberto na seção de [setup](../setup). O foco desta parte não é aprender a instalar o `cert-manager`, é aprender a usar.

## Criar recursos

```bash
kubectl apply -f parte06 --namespace default --kubeconfig kubeconfig
```

## Testar HTTPS

Para dar 100% certo (receber um certificado SSL de uma autoridade certificadora reconhecida internacionalmente), é necessário possuir um IP público. Como estamos rodando localmente, o máximo que vamos conseguir é um certificado SSL assinado pelo próprio cluster Kubernetes.

O erro "Autoridade Certificadora Inválida" é sinal de que, no ambiente local, funcionou na medida do possível. Qualquer outro erro significa que deu errado.

Para testar, acessar <https://aula.gces.com/>

## Deletar recursos

```bash
kubectl delete -f parte06 --namespace default --kubeconfig kubeconfig
```

## Diferenças para a parte05

```diff
diff --color -r '--exclude=README.md' parte05/django-ingress.yaml parte06/django-ingress.yaml
4a5,6
>   annotations:
>     cert-manager.io/issuer: exemplo
8a11,14
>   tls:
>   - hosts:
>     - aula.gces.com
>     secretName: ingress-exemplo
Only in parte06: django-issuer.yaml
```

Comando usado:

```bash
diff -r parte05 parte06 --exclude=README.md
```
