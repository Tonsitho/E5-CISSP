# E5-CISSP
DE STEPHANIS Antonio Rendu




<!-- PROJECT LOGO --> <br /> <div align="center"> <h3 align="center">Projet Docker : Applications Web</h3> <p align="center"> 
<a href="https://github.com/app-generator/django-soft-ui-dashboard"><strong>Documentation Django Soft UI Dashboard </strong></a> <br /> 
<a href="https://github.com/app-generator/flask-soft-ui-design">Documentation Flask Soft UI Design</a> · 
<a href="https://github.com/app-generator/ecommerce-flask-stripe">Documentation Ecommerce Flask Stripe</a> · 
<a href="https://github.com/app-generator/flask-material-dashboard.git">Documentation Flask Material DashBoard</a> </p> </div>

<!-- TABLE OF CONTENTS --> <details> <summary>Table des matières</summary> <ol> <li><a href="#structure-du-projet">Structure du projet</a></li> <li><a href="#configurations">Configurations</a></li> 
<li><a href="#etape-du-build">Étape du build</a></li> <li><a href="#logs">Logs</a></li> <li><a href="#quelques-interfaces">Quelques Interfaces</a></li> </ol> </details>



<!-- ABOUT THE PROJECT -->
## Struture du projet

Voici la structure du projet:

```bash
< PROJECT ROOT >
   |
   |-- apps/
   |    |-- django-soft-ui-dashboard/
   |    |-- flask-soft-ui-design/
   |    |-- ecommerce-flask-stripe/
   |    |-- rocket-django/
   |
   |-- nginx/
   |    |-- nginx.conf
   |
   |-- docker-compose.yml
   ************************************************************************
```


<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- FILES CONFIGURATIONS -->
## Configurations

. Contenu du fichier mynginxconf.conf

``` bash
# Django Soft UI Dashboard
upstream django-soft-ui {
    server django-soft-ui:8040;
}

server {
    listen 5005;
    server_name localhost;

    location / {
        proxy_pass http://django-soft-ui;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

# Flask Soft UI Design
upstream flask-soft-ui {
    server flask-soft-ui:8070;
}

server {
    listen 5008;
    server_name localhost;

    location / {
        proxy_pass http://flask-soft-ui;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

# Flask Material Dashboard
upstream ecommerce-flask-stripe {
    server ecommerce-flask-stripe:8060;
}

server {
    listen 5007;
    server_name localhost;

    location / {
        proxy_pass http://ecommerce-flask-stripe;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

# Flask Atlantis Dark
upstream rocket-django {
    server rocket-django:8050;
}

server {
    listen 5006;
    server_name localhost;

    location / {
        proxy_pass http://rocket-django;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

```

. Contenu du docker-compose.yml

``` bash
version: '3.8'

services:
  django-soft-ui:
    build: ./apps/django-soft-ui-dashboard
    ports:
      - "5080:5080"
    networks:
      - app_network

  flask-soft-ui:
    build: ./apps/flask-soft-ui-design
    ports:
      - "5083:5083"
    networks:
      - app_network

  flask-material-dashboard:
    build: ./apps/ecommerce-flask-stripe
    ports:
      - "5082:5082"
    networks:
      - app_network

  flask-atlantis-dark:
    build: ./apps/rocket-django
    ports:
      - "5081:5081"
    networks:
      - app_network

  nginx:
    image: nginx:latest
    ports:
      - "5080:5080"
      - "5081:5081"
      - "5082:5082"
      - "5083:5083"
    volumes:
      - ./nginx:/etc/nginx/conf.d
    depends_on:
      - django-soft-ui
      - flask-soft-ui
      - flask-material-dashboard
      - flask-atlantis-dark
    networks:
      - app_network

networks:
  app_network:
    driver: bridge

```

<!-- GETTING STARTED -->
## Etape du build

### Pour déployer les applications du répertoire "devoir":

1- Positionnez vous dans ce répertoire avec la commande suivante:

``` bash
cd devoir
```

2- Exécuter la commande suivante pour mettre en place votre iac:

``` bash
docker compose up -d
```

3- Après le build, tapez les commandes suivantes:

``` bash
docker images
docker ps
```

. Screen présentant les images

![alt text](screens/image.png)

``` bash
docker ps
```
ou
``` bash
docker ps -a
```
. Screen présentant les conteneurs en cours d'exécution (a update)

![alt text](screens/dockerps.png)

Testez vos applications en local sur les ports suivants: ( a update) 
  <ul>
    <li><a href="#http://localhost:5080">http://localhost:5080</a></li>
    <li><a href="#http://localhost:5081">http://localhost:5081</a></li>
    <li><a href="#http://localhost:5082">http://localhost:5082</a></li>

  </ul>

4- Pushez vos images sur le docker hub

. Connectez vous au docker hub:

``` bash
docker login
```

. Déplacer dans le répertoire de l'application pour exécuter les commandes suivantes:
``` bash
cd  nom_application
```

``` bash
docker build -t nom_image:tag_name .
```

``` bash
docker tag nom_image:tag: your_username/nom_image:tag_name_for_hub
```

``` bash
docker push your_username/nom_image:tag_name_for_hub
```


. Screen présentant les logs obtenus lors d'un push (a update)

![alt text](screen/Dashard.png)

. Docker Hub repositories (a update)

![alt text](screens/hub.png)

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- INTERFACES -->
## Quelques interfaces

. Soft UI Dashboard3

![alt text](screen/Dashboard.png)

. Soft UI Dashboard

![alt text](screen/SoftDashborad.png)

. Flask Materiaal Dashboard

![alt text](screen/flask.png)


## Choix des frameworks


Flask Soft UI Design

Léger et facile à utiliser.
Fournit une interface utilisateur moderne et personnalisable.

Ecommerce Flask Stripe

Simplifie l'intégration des paiements avec Stripe.
Idéal pour les projets de commerce électronique.

Rocket Django

Robuste et bien structuré pour des projets évolutifs.
Offre des fonctionnalités prédéfinies pour un développement rapide.
Ces frameworks sont légers, simples à prendre en main et proposent des exemples pratiques pour accélérer le développement tout en assurant une qualité professionnelle.

## Diagramme Projet

![alt text](screen/shema.png)
