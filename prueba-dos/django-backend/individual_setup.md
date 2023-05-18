## Para correr en ambiente local
### Build the Docker image
docker build -t django-app .
### Run the Docker container
docker run -d -p 8000:8000 django-app