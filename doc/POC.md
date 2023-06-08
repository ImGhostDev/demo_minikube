For POC, we decided to use ArgoCD as a graphical interface for CI.

1. Install `kubectl` and `minikube`:
```shell
brew install kubectl
brew install minikube
```

2. Run Minikube:
```shell 
minikube start
```

3. Create a namespace for ArgoCD:
```shell
kubectl create ns argocd
```

4. Apply the manifest for ArgoCD setup:
```shell
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

5. Wait until all services are running:
```shell
kubectl get pods -n argocd
```

6. Port forward the internal port of ArgoCD to your local machine:
```shell
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

7. Get the password for ArgoCD GUI (login as admin):
```shell
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

8. Click on "+ New App" in the ArgoCD GUI.

9. Set up the application name, project name, and choose whether to auto-create the namespace (if it hasn't been created before).

10. Configure the source. Provide your repository URL and the path to the necessary Helm chart or the deployment.yaml file.

11. Configure the destination. Use the default Kubernetes URL and specify the namespace (if it has been created before).

12. Click "Create," then "Sync," and you're done!