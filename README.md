### 1. Installation de ArgoCD

```bash
kubectl create namespace argocd
```
Puis je lance la commande suivante : 
```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Je reçois la réponse suivante : 
![image](https://github.com/user-attachments/assets/9d20dacb-8ae7-4942-b9c4-982c3ab2d47a)

### 2. Création de l'application ArgoCD

Je crée un fichier app.yaml :
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: mon-app
  namespace: argocd
spec:
  destination:
    namespace: default
    server: https://kubernetes.default.svc
  project: default
  source:
    repoURL: https://github.com/TON-UTILISATEUR/TON-FORK.git
    targetRevision: HEAD
    path: chemin/vers/le/dossier/k8s
  syncPolicy:
    automated:
      selfHeal: true
      prune: true
    syncOptions:
    - CreateNamespace=true
```
