# Dockerizing Applications
Here, we will be Dockerizing Applications, creating and building and Docker image for the same and pushing the docker image to the Docker hub repositories.

# Docker
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. 

Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allow you to run many containers simultaneously on a given host. Containers are lightweight and contain everything needed to run the application, so you do not need to rely on what is currently installed on the host. You can easily share containers while you work too.
You can learn more about the same in the [website.](https://docs.docker.com/get-started/overview/)

# What Is a Container
A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
You can learn more about the same in the [website.](https://www.docker.com/resources/what-container)


# What Is a Dockerizing
Dockerizing is the process of packing, deploying, and running applications using Docker containers. You can use Docker to pack your application with everything you need to run the application (such as libraries) and ship it as one package - a container. Containers are created from images that specify their precise contents.

# Installing Docker
> Here I am using AWS Amazon linux server
```sh
amazon-linux-extras install docker -y
systemctl restart docker.service
systemctl enable docker.service
```
Please see the [website](https://docs.docker.com/engine/install/) for more information.

# Flask Application

```sh
/root/Flask/
├── Dockerfile
└── project
    ├── app.py
    └── requirements.txt
```
- Created a folder "Flask" and added the Dockerfile and added the Flask application files inside a folder called "project" just like above.

```sh
vim Flask/project/app.py 
```
```sh
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
  return "<h1><center>This is Flask Application Version 1</center></h1>"

app.run(host='0.0.0.0', port=5000)
```
```sh
vim Flask/project/requirements.txt
```
```sh
flask
```
Here, in the directory "project" we added a simple flask application and defined the dependencies(flask) in the requirements.txt file that need to run this application.

```sh
vim Flask/Dockerfile
```
```sh
FROM alpine:latest
    
RUN  mkdir /tmp/pro-flask/

WORKDIR /tmp/pro-flask/

COPY ./project/  .

RUN apk update && apk add --no-cache python3 && apk add --no-cache py-pip

RUN pip install -r requirements.txt

EXPOSE 8081

CMD [ "python3" , "app.py"]
```


# NodeJS Application
```sh
/root/NodeJS/
├── Dockerfile
└── project
    ├── package.json
    └── server.js
```
- Created a folder "NodeJS" and added the Dockerfile and added the  application files inside a folder called "project" just like above.

```sh
vim NodeJS/project/package.json
```
```sh
{
  "name": "docker_web_app",
  "version": "1.0.0",
  "description": "Node.js on Docker",
  "author": "First Last <first.last@example.com>",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.16.1"
  }
}
```
```sh
vim NodeJS/project/server.js
```
```sh
'use strict';

const express = require('express');

// Constants
const PORT = 8081;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```
Here, in the directory "project" we added a simple NodeJS application.

```sh
vim NodeJS/Dockerfile
```
```sh
FROM node:16-alpine3.12

RUN  mkdir /tmp/node-js/

WORKDIR /tmp/node-js/

COPY ./project/  .

RUN npm install

EXPOSE 8081

CMD [ "node", "server.js" ]
```
