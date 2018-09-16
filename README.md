### GitLab Continuous Integration(CI/CD)
GitLab comes with built-in Continuous Integration, Continuous Deployment, and Continuous Delivery support to build, test, and deploy your application.
- https://docs.gitlab.com/ee/ci/README.html

### Git Runner
GitLab Runner is used to run your project's CI jobs and send the results back to GitLab.
- https://docs.gitlab.com/runner/

### Git Runner Executor
GitLab Runner implements a number of executors that can be used to run your builds in different scenarios, a better way is to use Docker as it allows to have a clean build environment, with easy dependency management (all dependencies for building the project could be put in the Docker image). The Docker executor allows you to easily create a build environment with dependent services, like MySQL. In `.gitlab-ci.ym.` with `image` keyword we can sepcify the docker image, which will be used to create a container on which your builds will be run.

### What this repostiroy provide
 Official images publieshed on Docker Hub just contain basic modules, so usually we want to extend it with customized modules for convenient usage. In this repository I contribute a docker image contained everything to build and deploy laravel project, the image contain php7.1.21 and required extensions for build laravel5.5, node version 10, ansible for deploying project to remote server.


I hope developers can contribute docker images used for other project's CI/CD (projects powered by Java,Python,Ruby etc.).

