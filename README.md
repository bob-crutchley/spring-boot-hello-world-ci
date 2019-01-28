# spring-boot-hello-world-ci
Automated CI setup using Docker

This project creates a basic CI pipeline for the [spring-boot-hello-world](https://github.com/bob-crutchley/spring-boot-hello-world) project 

## Project Components
There are two main components to this project, the NGINX and Jenkins services.

### NGINX
NGINX is a reverse proxy for Jenkins and the deployed application instances.
Both Jenkins and the spring boot servers can be accessed from the same host, just by changing the URL


### Jenkins
Jenkins is the CI tool that is going to be used to facilitate the automation for this project.


## Setup Guide
You will need Docker & Docker Compose installed for this project. 
This guide details how to configure Docker for Linux, if you are on Windows or Mac then you can use the install guide on the
Docker Hub Website and follow the install steps, Docker Compose will be installed this way as well -
[(Windows)](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
[(Mac)](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
.

#### How to install Docker for Linux
```bash
curl https://get.docker.com | sudo bash
```

#### How to install Docker Compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

#### The Pipeline can be created using docker-compose
The configurations for Docker Compose can be found in the `docker-compose.yaml` file. The file in this case defines a Jenkins and an NGINX service. Both of these are created when you run the command below.
```bash
docker-compose up -d
```

#### Accessing Jenkins
Jenkins will accessible from port 80 with the credentials set to admin:admin (it's best if you update this of course)

Because we are using Docker, we are able to deploy Jenkins preconfigured with the jobs already there.

To build the project and get it running, you can just the run the `spring-boot-hello-world` job that's there.

![Jenkins Home Page](docs/images/jenkins-home.png)

#### Feature Branches
The default branch being built by Jenkins is the master branch, to build another, change it in the job configurations. When a branch has been built with the included Jenkins job.
It can be accessed from `/spring-boot-hello-world/branch-name`

For example to connect to the deployed master branch:
`/spring-boot-hello-world/master`

#### Persisting Jobs
The jobs folder for Jenkins has been passed through the host machine as a bind mount. This essentially means that whatever jobs that you create, will be persisted to the host machine's disk in the project folder; `jenkins/jobs`. 

If you have forked this repository, you will be able to commit these changes to GitHub, meaning that you wont ever lose anymore Jenkins jobs that you create.

