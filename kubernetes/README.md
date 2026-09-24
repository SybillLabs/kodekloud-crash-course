<h1 align="center">
    ☸️ Kubernetes for beginners
</h1>

## `> quickstart`
- **Cours** : [Lien du cours](https://learn.kodekloud.com/learn/courses/crash-course-kubernetes-for-absolute-beginners)
- **Statut** : terminé le 07/09/2026
- **Environnement** : lab KodeKloud en ligne via interface web

![certificat](/kubernetes/assets/certificat.png)

## `> labs.sh`

Voici les différentes commandes Kubernetes que j'ai apprises dans ce cours, avec un petit exemple pour chacune d'entre elles :
```bash
# Affiche la liste des nodes du cluster
kubectl get nodes 
# Affiche les informations sur le cluster                      
kubectl cluster-info    
# Crée un pod avec l'image nginx                
kubectl run nginx-pod --image=nginx    
# Affiche la liste des pods du cluster   
kubectl get pods   
# Affiche la liste des pods du cluster avec plus d'informations                   
kubectl get pods -o wide  
# Crée un pod à partir d'un fichier YAML              
kubectl create -f pod-nginx.yaml 
# Affiche les informations détaillées sur un pod       
kubectl describe pod nginx-pod  
# Applique les modifications d'un fichier YAML à un pod existant        
kubectl apply -f pod-nginx.yaml         
```

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/kodekloud-crash-course.git"> Kodekloud - Crash Course</a></i>
</p>