<h1 align="center">
    ☸️ Kubernetes for beginners
</h1>

## `> overview.sh`
### C'est quoi Kubernetes et pourquoi l'utiliser ?

**Kubernetes** est un outil d'orchestration de conteneurs. Là où Docker gère des conteneurs sur une seule machine, Kubernetes les gère sur plusieurs serveurs à la fois : il décide où déployer chaque conteneur, le relance automatiquement s'il plante, répartit la charge entre les machines, et permet de scaler un service en ajoutant des instances à la demande.

Il existe d'autres outils d'orchestration (**Docker Swarm**, **Apache Mesos**), mais Kubernetes est devenu le standard de fait.

### C'est quoi un container et l'orchestration de containers ?

Un **container** (rappel du chapitre Docker) est une instance isolée d'une application, basée sur une image, qui partage le noyau de son hôte.

**Orchestrer des containers**, c'est automatiser tout ce qu'un humain devrait faire manuellement s'il gérait des dizaines de conteneurs à la main sur plusieurs machines : sur quel serveur le déployer, que faire s'il crashe, comment le faire communiquer avec les autres, comment répartir la charge si le trafic augmente. Kubernetes fait ce travail à la place de l'admin.

### C'est quoi les *Nodes* et un *cluster* ?

Les **Nodes** sont les serveurs sur lesquels les containers sont déployés. Deux types :
- **Master Node** (aussi appelé *Control Plane*) : gère les autres nodes, planifie où déployer chaque conteneur, surveille l'état du cluster. Il ne fait tourner aucun conteneur applicatif lui-même.
- **Worker Node** : exécute réellement les containers.

Un **cluster** est l'ensemble master node + worker nodes qui travaillent ensemble.

### C'est quoi un *Pod* ?

Un **Pod** est la plus petite unité déployable dans Kubernetes. Ce n'est pas un conteneur, c'est une enveloppe qui contient un ou plusieurs conteneurs partageant le même réseau et le même stockage.

Différence avec un container : le container est l'unité d'exécution (issue d'une image), le pod est l'unité de déploiement Kubernetes autour de ce container. La plupart du temps un pod contient un seul conteneur, mais Kubernetes autorise plusieurs conteneurs étroitement liés dans le même pod (ex. un conteneur principal et un conteneur annexe qui l'assiste).

Différence avec un node : le node est la machine physique/VM qui héberge les pods, le pod est ce qui tourne dessus.

Hiérarchie complète : **cluster → nodes → pods → containers**. Un cluster contient plusieurs nodes, chaque node peut héberger plusieurs pods, chaque pod contient un ou plusieurs containers.

Pour créer un container, un pod utilise une image, récupérée depuis un registry (Docker Hub par défaut).

### C'est quoi un fichier *YAML* ?

C'est le fichier de configuration utilisé pour créer, modifier ou supprimer des objets Kubernetes (pods, deployments, services...).

Un fichier YAML combine trois structures de données, pas des "versions" séparées :

- **Key-value pairs** : une propriété simple, une valeur.
```yaml
name: nginx-container
```
- **Array/Lists** : plusieurs valeurs pour une même propriété, ordonnées.
```yaml
containers:
  - name: nginx-container
  - name: sidecar-container
```
- **Dictionary** : des sous-propriétés imbriquées, non ordonnées.
```yaml
metadata:
  name: web-pod
  labels:
    app: web
```

Dans la pratique, on ne "choisit" jamais une seule structure pour tout un fichier. Un manifeste Kubernetes réel les imbrique systématiquement : `metadata` est un dictionary, qui contient `labels`, un autre dictionary, pendant que `containers` est une liste de dictionaries. C'est cette combinaison qui rend le YAML lisible pour des objets complexes.

⚠️ Les espaces comptent, jamais de tabulation. Indentation recommandée : 2 espaces. Une mauvaise indentation casse le fichier (voir exemple ci-dessous).

**Fichier YAML dans Kubernetes**
```yaml
apiVersion: v1        # Version de l'API Kubernetes utilisée pour créer l'objet
kind: Pod             # Type d'objet Kubernetes à créer
metadata:             # Informations sur l'objet (nom, labels...)
  name: web-pod
  labels:
    app: web
    env: prod
spec:                 # Configuration réelle de l'objet
  containers:
    - name: nginx-container
      image: nginx
```

## `> labs.sh`

Voici les différentes commandes Docker que j'ai apprises dans ce cours, avec un petit exemple pour chacune d'entre elles :
```bash
kubectl get nodes                       # Affiche la liste des nodes du cluster
kubectl cluster-info                    # Affiche les informations sur le cluster
kubectl run nginx-pod --image=nginx     # Crée un pod avec l'image nginx
kubectl get pods                        # Affiche la liste des pods du cluster
kubectl get pods -o wide                # Affiche la liste des pods du cluster avec plus d'informations
kubectl create -f pod-nginx.yaml        # Crée un pod à partir d'un fichier YAML
kubectl describe pod nginx-pod          # Affiche les informations détaillées sur un pod
kubectl apply -f pod-nginx.yaml         # Applique les modifications d'un fichier YAML à un pod existant
```


<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/kodekloud-crash-course.git"> Kodekloud - Crash Course</a></i> | <i>📍 From <a href="https://github.com/SybillLabs">SybillLabs</a></i>
</p>

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,100:0d0d0d&fontColor=FF003C&fontSize=50&height=100&width=900&text=%5BEOF%5D&section=footer"/>
</p>