<h1 align="center">
    🐋 Docker for beginners
</h1>

## `> quickstart`
- **Cours** : [Lien du cours](https://learn.kodekloud.com/learn/courses/crash-course-docker-for-absolute-beginner)
- **Statut** : terminé le 04/08/2026
- **Environnement** : lab KodeKloud en ligne via interface web

![certificat](/docker/assets/certificat.png)

## `> labs`

Voici les différentes commandes *Docker* que j'ai apprises dans ce cours, avec un petit exemple pour chacune d'entre elles :
```bash
# Lab -- docker run
# Afficher l'aide de Docker et la liste des sous-commandes disponibles
docker --help   
# Exécute une instance du conteneur Ubuntu en arrière-plan, le télécharge si introuvable localement                        
docker run ubuntu   

# Lab -- docker ps, stop
# Affiche la liste des conteneurs en cours d'exécution 
docker ps   
# Affiche la liste de tous les conteneurs, y compris ceux qui sont arrêtés                           
docker ps -a   
# Arrête un conteneur en cours d'exécution                         
docker stop <container_name>        

# Lab -- docker rm, rmi
# Affiche la liste des images disponibles localement
docker images   
# Supprime un conteneur arrêté, possibilité de supprimer plusieurs conteneurs en même temps                        
docker rm        
# Supprime une image locale, possibilité de supprimer plusieurs images en même temps                       
docker rmi                              

# Lab -- docker pull, exec
# Télécharge une image depuis une registry publique (Docker Hub par défaut)
docker pull       
# Exécute un conteneur nommé "webapp" en arrière-plan à partir de l'image nginx:1.14-alpine                      
docker run -d --name webapp nginx:1.14-alpine
# Exécute une commande dans un conteneur en cours d'exécution
docker exec 
# Ajoute une ligne de texte dans un fichier à l'intérieur du conteneur
docker exec <container_id> sh -c 'echo "Hello from inside the container!" >> /home/hello.txt'
# Affiche l'ID des conteneurs en cours d'exécution basés sur l'image Ubuntu
docker ps --filter ancestor=ubuntu --format '{{.ID}}'
```

---

<p align="center">  
    <i>↪️ Back to<a href="https://github.com/SybillLabs/kodekloud-crash-course.git"> Kodekloud - Crash Course</a></i>
</p>