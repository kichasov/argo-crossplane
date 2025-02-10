Crossplane ArgoCD POC

1) kubectl apply -k argocd/install  
2) kubectl wait --for=condition=ready pod -l app.kubernetes.io/name=argocd-server --namespace argocd --timeout=300s  
3) kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo  
4) kubectl apply -f argocd/crossplane-bootstrap/crossplane-helm-secret.yaml  
5) kubectl apply -n argocd -f argocd/crossplane-bootstrap/crossplane.yaml  
6) kubectl apply -f providers-and-functions/provider-kubernetes.yaml  
7) kubectl apply -f providers-and-functions/provider-helm.yaml  
8) kubectl apply -f providers-and-functions/provider-kubernetes-config.yaml  
9) kubectl apply -f providers-and-functions/provider-helm-config.yaml  
10) kubectl apply -f providers-and-functions/functions.yaml  
11) kubectl create namespace jaeger  
12) kubectl create -n jaeger secret docker-registry ghcr-io-secret --docker-username="GitHub_Username" --docker-password="GutHub_Password" --docker-server='https://ghcr.io/v1/'  
kubectl apply -f infrastructure-bootstrap.yaml  
(replace with your values)
13) kubectl patch deploy app-springboot-helm-chart -n robot-shop -p '{"spec": {"template":{"metadata":{"annotations":{"instrumentation.opentelemetry.io/inject-java":"true"}}}} }'  
