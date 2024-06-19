# docker-hub

# Docker Hub

Ce guide décrit la procédure pour héberger votre image Docker sur Docker Hub.

## Procédure pour pousser une application Django sur Docker Hub

1. Créez un fichier `Dockerfile` au même niveau que `manage.py` et remplissez-le avec les instructions suivantes :

   ```dockerfile
   # Use the official Python image as a parent image
   FROM python:3.11-slim-bullseye

   # Set environment variables
   ENV PYTHONDONTWRITEBYTECODE 1
   ENV PYTHONUNBUFFERED 1

   # Set the working directory in the container
   RUN mkdir /app 
   WORKDIR /app

   # Copy the dependencies file to the working directory
   COPY requirements.txt /app/

   # Install any dependencies
   RUN pip install --upgrade pip
   RUN pip install -r requirements.txt

   # Copy the rest of the application code to the working directory
   COPY . /app/
    
   EXPOSE 8000
   CMD [ "python", "manage.py", "runserver", "0.0.0.0:8000"]

   ```

2. Créez l'image de votre projet :

   ```bash
   docker build -t nom-image .
   ```

3. Testez l'image créée :

   ```bash
   docker run -p 8000:8000 nom-image
   ```

4. Connectez-vous à votre compte Docker Hub :

   ```bash
   docker login
   ```

5. Vérifiez l'image créée :

   ```bash
   docker images
   ```

6. Déployez l'image sur Docker Hub :

   ```bash
   docker tag nom-image:latest nom-utilisateur/nom-image
   # Exemple : docker tag joel-django-crud1 joelandedi/joel-django-crud1

   docker push nom-utilisateur/nom-image
   # Exemple : docker push joelandedi/joel-django-crud1
   ```

Assurez-vous d'avoir remplacé `nom-image`, `nom-utilisateur`, et les autres valeurs par celles correspondant à votre application Django et à votre compte Docker Hub.
