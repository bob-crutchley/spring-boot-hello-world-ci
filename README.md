# spring-boot-hello-world-ci
Automated CI setup using Docker

The Pipeline can be created using docker-compose:
```bash
docker-compose up -d
```
Jenkins will accessible from port 80

When a branch has been built with the included Jenkins job
It can be accessed from `/spring-boot-hello-world/branch-name`
For example to connect to the deployed master branch:
`/spring-boot-hello-world/master`

