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
![image](https://github.com/user-attachments/assets/31142150-f9e2-4101-a2ba-e51e13e83695)

Je lance avec la commande suivante : 
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
![image](https://github.com/user-attachments/assets/77660295-3a93-41f1-ae8b-8acae996596d)

Et lorsque j'essaie d'accèder à la page web via l'URL `127.0.0.1:8080` je vois ceci : 

![image](https://github.com/user-attachments/assets/3385f6aa-b72b-4101-aeb9-a70552ba6b10)

