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

#### ERROR:

Failed: Angular could not be found on the page http://test:4200/. If this is not an Angular application, you may need to turn off waiting for Angular. Please see https://github.com/angular/protractor/blob/master/docs/timeouts.md#waiting-for-angular-on-page-load

The error seems misleading since the same error is thrown if there is some issue with protractor test or if the base url is not accessible. Since the test runs perfectlyfine on local the issue is with accessing the URL which is a container communication issue.

Here test is the reference to the duplicate angular container which is spun for testing. Containers can communicate using names used in docker-compose file.

Duplicate container is used since angular container refers to Selenium Hub and hence hub cannot refer back to angular otherwise there would be a cyclic dependency in docker-compose. Hence duplicate angular container is spun to allow hub to access that for testing. But still the error persists.

Reference for Angular App : https://coursetro.com/posts/code/84/Setting-up-an-Angular-4-MEAN-Stack-(Tutorial)
