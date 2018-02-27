# Automated_testing_in_Docker_container
Automated functional testing of Angular application using Selenium inside Docker container

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

## OPEN ISSUES

The communication between the Selenium and Angular container works using the static IP as seen in the "protractor.conf.js" file. The issue to figure out is, why Docker is not able to resolve the service name to the IP address (to reach angular container using service name and not static IP), when all the posts on the Internet say so.

Infact, I also tried to bringup an nginx server using docker-compose to run the ping command from there. I pinged the angular container using the service name "angular" and it was able to successfully communicate and receive data. But it is not able to run the ping command itself on the selenium server; which avoids confirmation that the selenium is able to locate angular or not. 

#### ERROR:

Failed: Angular could not be found on the page http://test:4200/. If this is not an Angular application, you may need to turn off waiting for Angular. Please see https://github.com/angular/protractor/blob/master/docs/timeouts.md#waiting-for-angular-on-page-load

The error seems misleading since the same error is thrown if there is some issue with protractor test or if the base url is not accessible. Since the test runs perfectly fine on local the issue is with accessing the URL which is a container communication issue.

Here test is the reference to the duplicate angular container which is spun for testing. Containers can communicate using names used in docker-compose file.

Duplicate container is used since angular container refers to Selenium Hub and hence hub cannot refer back to angular otherwise there would be a cyclic dependency in docker-compose. Hence duplicate angular container is spun to allow hub to access that for testing. But still the error persists.

##### Some helpful links

https://medium.com/@zhao.li/end-to-end-testing-angular-with-protractor-selenium-in-containers-d631edcbf13

https://michelesr.github.io/thesis/dist/thesis.pdf

Reference for Angular App : https://coursetro.com/posts/code/84/Setting-up-an-Angular-4-MEAN-Stack-(Tutorial)
