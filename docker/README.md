<h1 align="center">
    🐋 Docker for beginners
</h1>

## `> overview.sh`
- **C'est quoi un conteneur?**  
    Un conteneur est un environnement isolé qui exécute une application en s'appuyant sur le noyau du système d’exploitation de l'hôte. Cette approche le rend beaucoup plus léger et rapide qu’une machine virtuelle, qui elle embarque son propre système d’exploitation complet.
- **Est-ce que je peux faire tourner un CT Windows sous un hôte Linux ?**  
    Non. Un conteneur doit utiliser le même type de système d'exploitation que son hôte : un conteneur Linux ne peut pas fonctionner sur un hôte Windows, et inversement.
- **Que sont les `images` et les `registries` ?**  
    Une `image` est un ensemble de fichiers contenant tout ce qu'il faut pour exécuter une application dans un conteneur : code, dépendances, bibliothèques, configuration.  
    Une `registry` est un service qui stocke et distribue ces images. On peut y récupérer des images publiques (comme sur Docker Hub) ou y publier ses propres images.
- **Quel différence entre `images`et `containers` ?**  
    Une `image` est un modèle statique, un fichier qui contient tout ce qu’il faut pour créer un conteneur.  
    Un `container` est une instance en cours d'exécution d’une image. On peut créer plusieurs conteneurs à partir de la même image.
- **C'est quoi le rôle moteur Docker ?**  
    `Docker Engine` est le service qui permet de créer, exécuter et gérer les conteneurs à partir des images.
- **Comment fonctionne le réseau dans Docker ?**  
    Par défaut, Docker crée un réseau interne permettant aux conteneurs de communiquer entre eux ou avec l'extérieur selon la configuration choisie.
- **Pourquoi mes données disparaissent quand je supprime un conteneur ?**  
    Les données d'un conteneur ne sont pas persistantes par défaut; pour conserver les fichiers, on utilise des volumes.
- **Quels sont les avantages d’un container par rapport à une VM ?**  
    - Démarrage très rapide
    - Consommation de ressources réduite
    - Isolation des processus, du réseau et du système de fichiers
    - Portabilité élevée (fonctionne sur tout hôte compatible)
- **Quels sont les inconvénients d’un container par rapport à une VM ?**
    - Sécurité plus limitée (partage du noyau de l’hôte)
    - Pas de support multi‑OS (un conteneur doit correspondre au type d’OS de l’hôte)
    - Écosystème moins mature que celui de la virtualisation classique

## `> labs.sh`

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