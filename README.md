# API MERN STACK - DOCKER

Simple API using MERN stack and Docker.
Client project using endpoints for: 
  * Authentification: Signup / Login
  * Article: CRUD system


### Pré-requis

What you need to use it:
  * GitHub
  * Docker

### Installation

Step to install:
  1. ``` git clone https://github.com/AlexandreHoumeau/Houmeau_Alexandre_M1_2020_docker.git ```
  2. ``` docker-compose up ```
  3. Go to ``` http://localhost:3000/ ```

### Using the application

You can create an account by register.
Or, by launching the app with ``` docker-compose up ``` the database is filled with a user:
  * email: Hello@gmail.com
  * password: test

## SETUP

#### DOCKER SETUP
***frontend/Dockerfile***
````
FROM mhart/alpine-node:12
WORKDIR /frontend/
COPY . /frontend/
RUN npm install
EXPOSE 3000
CMD [ "npm", "start" ]
````


***backend/Dockerfile***
````
FROM node:10
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 8080
CMD [ "node", "server.js" ]
````


***mongo_seed/Dockerfile***
````
FROM mongo:latest
COPY init.json /init.json
CMD  mongoimport --host mongo --db=messageNode --collection=users --drop --type json --file /init.json --jsonArray
````
***docker-compose.yml***
````
version: "3"
services:
  api:
    container_name: api_message_node
    build: ./backend
    restart: always
    ports:
      - 8080:8080
    depends_on:
      - mongo
  mongo:
    image: mongo:3.6
    expose:
      - 27017
    ports:
      - 27017:27017
  mongo-seed:
    build: ./mongo_seed
    depends_on:
      - mongo 

  frontend:
    container_name: client
    build: frontend
    ports:
      - "3000:3000"
````

## Docker Hub
This project can be found on ***Docker Hub***

#### Docker Hub Setup
***Backend setup:***
 * ````docker login --username USERNAME --password PASSWORD````
 * ````docker build -t backend:1.0````
 * ````docker tag imageID repositoryID/backend:1.0 ````
 
 ***Frontend setup:***
 * ````docker build -t frontend:1.0````
 * ````docker tag imageID repositoryID/frontend:1.0 ````
 
 ***Mongo Seed setup:***
 * ````docker build -t mongo_seed:1.0````
 * ````docker tag imageID repositoryID/mongo_seed:1.0 ````
 
 

