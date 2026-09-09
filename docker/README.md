<h1 align="center">
    🐋 Docker for beginners
</h1>

## `> overview.sh`

### Qu'est-ce que Docker et pourquoi l'utiliser ?

Docker permet de faire tourner plusieurs services isolés sur une seule machine, sans les faire cohabiter en vrac sur le même OS.

Un **conteneur** est un environnement isolé qui exécute une application en s'appuyant sur le noyau de l'hôte. Contrairement à une VM qui embarque son propre OS complet, le conteneur partage le noyau de la machine hôte : plus léger, démarrage quasi instantané, mais isolation plus faible qu'une VM (si le noyau hôte plante, tous les conteneurs tombent avec).

> ⚠️ Un conteneur doit être du même type d'OS que son hôte. Pas de conteneur Windows sur un hôte Linux, et inversement.

**Pourquoi Docker et pas juste installer les services directement sur l'hôte ?**
- Chaque service garde ses propres dépendances (versions, libs) sans conflit avec les autres.
- Reproductibilité : l'environnement est versionné (`Dockerfile`), redéployable à l'identique sur une autre machine.
- Portabilité : ça tourne pareil en dev, en test, en prod.

### VM vs Conteneur : que choisir ?

| Besoin | Solution |
|---|---|
| Isolation forte (kernel séparé, panne d'un service ne doit rien impacter d'autre) | VM ou machine dédiée |
| Isolation logique suffisante (services de criticité comparable, juste éviter les conflits de dépendances) | Une machine + Docker, un conteneur par service |

- *Exemples d'isolation forte requise* : Active Directory, DHCP/DNS primaire, base de données réglementée, firewall.
- *Exemples d'isolation logique suffisante* : wiki interne, monitoring, environnements de test, outils de dev.

**Question à se poser pour trancher :** si ce service tombe ou est compromis, quel est le rayon de dégât acceptable ? 
- Impact large ou obligation réglementaire → VM. 
- Impact isolé et tolérable → conteneur.

### Images, containers, registry, engine

- **Image** : modèle statique, contient tout pour créer un conteneur (code, dépendances, config).
- **Registry** : stocke et distribue les images (ex. Docker Hub).
- **Docker Engine** : le service qui crée, exécute et gère les conteneurs à partir des images.

### Réseau et persistance

- Par défaut, Docker crée un réseau interne pour la communication entre conteneurs et vers l'extérieur.
- Les données d'un conteneur ne sont **pas persistantes** par défaut : à la suppression du conteneur, tout disparaît. Pour conserver des fichiers, on utilise des **volumes**.

## `> labs.sh`

Voici les différentes commandes Docker que j'ai apprises dans ce cours, avec un petit exemple pour chacune d'entre elles :
```bash
# Lab -- docker run
docker --help                           # Afficher l'aide de Docker et la liste des sous-commandes disponibles
docker run ubuntu                       # Exécute une instance du conteneur Ubuntu en arrière-plan, le télécharge si introuvable localement
# Lab -- docker ps, stop
docker ps                               # Affiche la liste des conteneurs en cours d'exécution
docker ps -a                            # Affiche la liste de tous les conteneurs, y compris ceux qui sont arrêtés
docker stop <container_name>            # Arrête un conteneur en cours d'exécution
# Lab -- docker rm, rmi
docker images                           # Affiche la liste des images disponibles localement
docker rm                               # Supprime un conteneur arrêté, possibilité de supprimer plusieurs conteneurs en même temps
docker rmi                              # Supprime une image locale, possibilité de supprimer plusieurs images en même temps
# Lab -- docker pull, exec
docker pull                             # Télécharge une image depuis une registry publique (Docker Hub par défaut)
docker run -d --name webapp nginx:1.14-alpine
                                        # Exécute un conteneur nommé "webapp" en arrière-plan à partir de l'image nginx:1.14-alpine
docker exec                             # Exécute une commande dans un conteneur en cours d'exécution
docker exec <container_id> sh -c 'echo "Hello from inside the container!" >> /home/hello.txt'
                                        # Ajoute une ligne de texte dans un fichier à l'intérieur du conteneur
docker ps --filter ancestor=ubuntu --format '{{.ID}}'
                                        # Affiche l'ID des conteneurs en cours d'exécution basés sur l'image Ubuntu                     
```

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/kodekloud-crash-course.git"> Kodekloud - Crash Course</a></i> | <i>📍 From <a href="https://github.com/SybillLabs">SybillLabs</a></i>
</p>

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,100:0d0d0d&fontColor=FF003C&fontSize=50&height=100&width=900&text=%5BEOF%5D&section=footer"/>
</p>