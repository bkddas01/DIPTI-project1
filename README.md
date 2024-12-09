
# Task 1

### Step 1: Create the index.html File
Create a simple index.html file to serve via the Nginx server\
File: **index.html**




```bash
  <!doctype html>
<html>
 <body style="backgroud-color:rgb(49, 214, 220);"><center>
    <head>
     <title>Docker Project</title>
    </head>
    <body>
     <p>Welcome to my Docker Project!<p>
        <p>Today's Date and Time is: <span id='date-time'></span><p>
        <script>
             var dateAndTime = new Date();
             document.getElementById('date-time').innerHTML=dateAndTime.toLocaleString();
        </script>
        </body>
</html>

```
### Step 2: Create the Dockerfile
This Dockerfile uses the Nginx base image and serves the index.html file by copying it into the Nginx HTML directory.

```bash
FROM nginx
COPY index.html /usr/share/nginx/html
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]

```
### Step 3: Build and Run the Docker Image
1. Save the index.html and Dockerfile in the same directory.
2. Open a terminal, navigate to this directory, and build the Docker image:

```bash
docker build -t nginx_bkd .
```
3. Run the Docker container

```bash
docker run -d --name web-server -p 8080:80 nginx_bkd
```
4. Access the webpage by opening a browser and visiting

```bash
http://localhost:8080
```
### Step 4: Push the docker image into DockerHub

```bash
docker tag nginx_bkd:latest bkddas/docker_images

docker login

docker push bkddas/docker_images
```
