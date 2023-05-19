
# Despliegue de una aplicación Django y React.js

Este repositorio contiene los archivos necesarios para el despliegue dockerizado de una aplicación web con backend en Django y frontend en React.js. A continuación, se proporcionan instrucciones detalladas para compilar y desplegar la aplicación tanto en una PC local como en la nube utilizando AWS o GCP.

## Requisitos previos

Tener instalados los siguientes componentes:

Docker: [Instalación de Docker](https://docs.docker.com/get-docker/) 
Docker Compose: [Instalación de Docker Compose](https://docs.docker.com/compose/install/) 

## Compilación y despliegue local

 1. Clonar repositorio: `git clone <URL_DEL_REPOSITORIO>`
 2. Navegar al directorio del docker-compose: `cd <NOMBRE_DEL_REPOSITORIO>/prueba-dos/`
 3. Ejecutar: `docker-compose up --build`
 4. Acceder a los servicios:
	 - App Django: `[localhost:8000](http://localhost:8000/)`
	 - App React: `[http://localhost](http://localhost:80/)`
 
> Asegurarse de tener disponibles los puertos 80 y 8000

Enjoy :)


## Compilación y despliegue en la nube (GCP)
#### Prerequisitos:
 - Tener cuenta gcp y configurar credenciales de entorno y acceso al proyecto
#### Config, Build & Deploy:
 1. Crear archivo de config en el dir raiz `cloudbuild.yaml` que buildee las imagenes de ambos contenedores usando docker-compose. Usar tags para su publicacion en  Artifact Registry o Container Registry (no recomendado, en mayo/2024 no poseera más soporte)
Por ejemplo (no testeado):
````    
steps:
  - name: 'docker/compose:1.29.2'
    args:
      - '-f'
      - 'docker-compose.yml'
      - 'build'
  - name: 'docker/compose:1.29.2'
    args:
      - '-f'
      - 'docker-compose.yml'
      - 'up'
      - '-d'
images:
  - 'gcr.io/$PROJECT_ID/django-backend'
  - 'gcr.io/$PROJECT_ID/react-frontend'
````
 2. Implementar las instancias de Cloud Run utilizando las imagenes recién publicadas.
