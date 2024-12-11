
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

To deploy your container to a Kubernetes cluster using a NodePort service, follow these steps:
# Step 5: Create a Kubernetes Deployment

The Deployment will ensure your container is running and can manage updates. Save the following YAML as\
*deployment.yaml*

```bash
  apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: myproject
  name: myproject
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myproject
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: myproject
    spec:
      containers:
      - image: bkddas/docker_images:latest
        name: myproject

```
### Step 6: Create a NodePort Service
#### The NodePort service will expose your container to a port on the cluster nodes. Save this YAML as service.yaml

```bash
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: myproject
  name: web-server
spec:
  ports:
  - name: "8080"
    port: 8080
    protocol: TCP
    targetPort: 80
  selector:
    app: myproject
  type: NodePort

```
### Step 7: Apply the YAML Files
#### Run the following commands to deploy the container:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Step 8: Access the Application
#### Access the application using the node's IP and the NodePort

```bash
http://<node-ip>:"NodePort port number"
```












