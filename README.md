# Automated_testing_in_Docker_container
Automated functional testing of Angular application using Selenium inside Docker container

## Steps to run with Docker Swarm

1) Bring Docker Swarm up
docker swarm init

2) Run the docker-compose file on the Docker swarm
docker stack deploy --compose-file docker-compose.yml angular4mean

3) Check if the processes are running
docker ps

4) Run Test Command inside angular container
docker exec -it <container id for angular container> npm test

#### To make changes to the angular container:
1) Enable the commented part in the docker-compose file to build the angular container from local.

2) Run docker-compose build - to build the new container

3) Tag the new image to the repository on Docker Hub
docker tag angular4mean_angular ruchitgandhi/angular_mean:test

4) Push the new image to Docker Hub
docker push ruchitgandhi/angular_mean

#### Some Helpful Links:
https://medium.com/webpack/webpack-dev-server-middleware-security-issues-1489d950874a

https://docs.docker.com/compose/networking/

https://docs.docker.com/engine/swarm/stack-deploy/

#### Using VNC Viewer to Debug the Docker Chromenode
Open VNC Viewer and log in to host "localhost:5900" with the common password "secret" and you can see the anular webpage insdie the Google Chrome there.

## Steps to run on Local

#### Note: Will have to make changes to protractor.conf.js to remove link to selenium hub address and fix the localhost address.

npm start
npm test (in another cmd)

## Steps to run dockerised version

1) docker-compose up --build -d
(This will build and start all docker containers)

2) docker-compose run angular npm test
(This will pass npm test command to the angular container to run selenium tests. Future prospect is to run this command with startup of containers.)

OR

2) docker exec -it <CONTAINER_ID of Angular container> npm test
(Container id can be found using command docker ps)

##### Some helpful links

https://medium.com/@zhao.li/end-to-end-testing-angular-with-protractor-selenium-in-containers-d631edcbf13

https://michelesr.github.io/thesis/dist/thesis.pdf

Reference for Angular App : https://coursetro.com/posts/code/84/Setting-up-an-Angular-4-MEAN-Stack-(Tutorial)
