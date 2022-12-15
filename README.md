
**Projet DevOps**

# Tp-Docker

**5. Exécuter un serveur web (apache, nginx, …) dans un conteneur docker** 

*  a. Récupérer l’image sur le Docker Hub

 >docker pull nginx
  
*  b. Vérifier que cette image est présente en local
>docker image
  
*  c. Créer un fichier index.html simple
>insérer image fichier
  
*  d. Démarrer un conteneur et servir la page html créée précédemment à l’aide d’un volume (option -v de docker run)
>docker run --name vol-1 -p 80:80 -v /root/docker:/usr/share/nginx/html:ro -d nginx
  
*  e. Supprimer le conteneur précédent et arriver au même résultat que précédemment à l’aide de la commande docker cp
>docker ps -a

>docker rm mon_conteneur_id

>docker cp /root/docker/index.html mon_conteneur_id/usr/share/nginx/html
  

**6. Builder une image** 

*  a. A l’aide d’un Dockerfile, créer une image (commande docker build)
 
>FROM nginx:latest
>COPY index.html /usr/share/html

>docker build -t <nom-de_l'image>
  
*  b. Exécuter cette nouvelle image de manière à servir la page html (commande docker run) 

>docker run -p 90:80 -d nginx:latest
  
  c. Quelles différences observez-vous entre les procédures 5. et 6. ? Avantages et inconvénients de l’une et de l’autre méthode ? (Mettre en relation ce qui est observé avec ce qui a été présenté pendant le cours)
  
  -- 
  
  
**7. Utiliser une base de données dans un conteneur docker**

*  a. Récupérer les images mysql:5.7 et phpmyadmin/phpmyadmin depuis le Docker Hub 

>docker pull mysql:5.7
  
>docker pull phpmyadmin
  
  
  
*  b. Exécuter deux conteneurs à partir des images et ajouter une table ainsi que quelques enregistrements dans la base de données à l’aide de phpmyadmin
 
>docker run --name mysql_container -p 3306:3306 -e MYSQL_DATABASE=ynov -e MYSQL_USER=user -e MYSQL_PASSWORD=nathan -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:5.7

>docker exec -it mysql_container bash
  
>docker run --name phpmyadmin_container --link mysql_container -e PMA8HOST=mysql_container -p 8080:80 phpmyadmin
 
>docker ps

>docker start phpmyadmin_container
  
    - ajout table dans container - methode graphique depuis l'interface
    
>docker exec -it id_mysql -u root -p


**8. Faire la même chose que précédemment en utilisant un fichier docker-compose.yml** 

*  a. Qu’apporte le fichier docker-compose par rapport aux commandes docker run ? Pourquoi est-il intéressant ? (cf. ce qui a été présenté pendant le cours) 
 
 
  * b. Quel moyen permet de configurer (premier utilisateur, première base de données, mot de passe root, …) facilement le conteneur mysql au lancement ?
  

**9. Observation de l’isolation réseau entre 3 conteneurs** 

* a. A l’aide de docker-compose et de l’image praqma/network-multitool disponible sur le Docker Hub créer 3 services (web, app et db) et 2 réseaux (frontend et backend). Les services web et db ne devront pas pouvoir effectuer de ping de l’un vers l’autre 


    
* b. Quelles lignes du résultat de la commande docker inspect justifient ce comportement ? 

* c. Dans quelle situation réelles (avec quelles images) pourrait-on avoir cette configuration réseau ? Dans quel but ?
  
