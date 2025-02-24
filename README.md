# 🐳 Docker

Docker is a software platform that simplifies the process of building, running, managing & distributing application.

### 🐳 Docker installation 🔗

    https://www.youtube.com/watch?v=Z6SLxKZicQc

For command below 🔗

    https://docs.docker.com/desktop/install/ubuntu/

source 2 :

    https://www.youtube.com/watch?v=5_EA3rBCXmU&t=197s

cmd :

    sudo apt-get update
    cd Downloads // go to the docker desktop download folder
    ls
    sudo apt-get install ./<name_of_the_package> //<name_of_the_package> = docker-desktop-4.28.0-amd64.deb
    systemctl --user start docker-desktop

### 🐳 Docker course 🔗

Source 1 :

    https://www.youtube.com/playlist?list=PL8p2I9GklV47v6WZTjHAqdsHxpTIpjRwn

Source 2 :

    https://www.youtube.com/watch?v=31k6AtW-b3Y
    https://www.youtube.com/watch?v=xPT8mXa-sJg

### step-1: Component of Dockerfile

file name - dockerfile

    FROM node:latest                // which language
    RUN npm install -g nodemon      //install nodemon for instant change
    WORKDIR /app                    // storing directory
    COPY . .                        // source & destination
    RUN npm install                 // install all dependencies
    EXPOSE 8000                     // running port of app
    CMD [ "nodemon", "index.js" ]   // running command

### step-2: Docker ignore file

file name - .dockerignore

    node_modules
    *.txt

If we want to ignore all files that has '.txt' extention then simply use above method, this will work for all extention

### step-3: Login into docker

    docker login -u <user_name>

### step-4: Create an image for an app in docker

After complete the above steps.Suppose my app name is dockertest & i used "image_name" also as dockertest.You can choose your "image_name".

Syntax :

    docker build -t <image_name> <image folder>

Example :

    docker build -t dockertest-image .

Here "." means current folder

![Image](https://github.com/user-attachments/assets/338b1d2a-cacb-488d-b3a1-d8e5d51e683f)

### step-5: Create a container using above image name

Syntax :

    docker run -it <image_name>

Example :

    docker run -it dockertest-image

if "image_name" not found in the docker then it will pull the image from the "hub.docker.com" if "image name" existed in "hub.docker"

### step-6: Port mapping

If want to run this container in your local server. Need to mapping the port

    docker run -it -p 8001:8001 dockertest-image

you can marge the step 4 & 5 like step 5

![Screenshot from 2024-03-30 14-58-48](https://github.com/s0urav6529/softcopy-note/assets/96060029/63d79be8-05c2-476a-a13c-3728be6045cd)

### step-7: Go to the root of container & do other staffs

    docker exec -it <container_id> bash

![Screenshot from 2024-03-30 15-01-07](https://github.com/s0urav6529/softcopy-note/assets/96060029/274d69eb-e9d6-4393-8aab-5daad8e88b8a)

### Pass the environment variable

Suppose in my code my port is 8000, but further i want that my port must be 4000, due to some reason. So, i can pass the environment variable.

![Screenshot from 2024-03-30 15-03-43](https://github.com/s0urav6529/softcopy-note/assets/96060029/a42f358d-30ef-49d0-9493-232ecf2fcb44)

### Push in hub.docker

If want to push my code in docker hub. Then need to create a repository in the hub.docker & copy the "image_name" from the repositoty.
Copy the "image_name" and create a build locally.

step : 1

![Screenshot from 2024-03-30 15-17-06](https://github.com/s0urav6529/softcopy-note/assets/96060029/b232dd48-c1ba-4d7a-ab3b-2b34872b3221)

step 2 :

![Screenshot from 2024-03-30 15-17-48](https://github.com/s0urav6529/softcopy-note/assets/96060029/5569a128-a26d-409c-ae2c-4f04f739a22b)

step 3 :

![Screenshot from 2024-03-30 15-19-45](https://github.com/s0urav6529/softcopy-note/assets/96060029/e9dae6db-fb48-47d4-a67a-2eb18d2b2c3d)

If not login in hub.docker in locally, then need to login & run this command again

![Screenshot from 2024-03-30 15-23-01](https://github.com/s0urav6529/softcopy-note/assets/96060029/0427ca5c-94ff-4b7c-a407-905264420e0d)

### Run image directly using cmd

    docker run dockertest

### Delete images & containers

For display all images

    docker images
    docker image ls

Normally delete an image

    docker image rm <image name>

For force-fully delete a image, if that image already in use by any container

    docker image rm <image name> -f

For display all containers

    docker ps -a

Normally delete an container

    docker container rm <container name>

For force-fully delete a container, if that container is on running

    docker container rm <container name> -f

### Delete all images & container at a time

    docker system prune -a

### Create image using version

Syntax :

    docker build -t <image name>:<version> <image folder>

Here, 'image name' like dockertest-image, 'version' v1,v2 etc & 'image folder' like '.'

Example :

    docker build -t dockertest-image:v2 .

### Run image container version in cmd

Syntax :

    docker run --name <conatainer name>-<version> -p <port1>:<port2> <image name>:<version>

Here, 'container name' like dockertest-container, 'version' like v1,v2 etc, 'port1' 5001, 'port2' as your docker port & 'image name' like dockertest-image

Example :

    docker run --name dockertest-container-v2 -p 5501:8000 dockertest-image:v2

### Run image container volumn in cmd

    docker run --name dockertest-container-v2 -p 5501:8000 --rm -v /home/sourav/dockertest:/app dockertest-image:v2

Here --rm remove the current container and create a new container, -v is volumn & '/home/sourav/dockertest' is the root path of 'index.js' file & '/app' is the working directory.

### Compose File in Docker

file name - compose.yaml

    services:
        img:
            build: .
            container_name: dockertest-container
            ports:
            - 5501:8000

### Run below command for create a continer

    docker compose up

### Share image on docker hub

Docker hub is a repository of docker images. Where many public images are available.