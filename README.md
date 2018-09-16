### GitLab Continuous Integration(CI/CD)
GitLab comes with built-in Continuous Integration, Continuous Deployment, and Continuous Delivery support to build, test, and deploy your application.
- https://docs.gitlab.com/ee/ci/README.html

### Git Runner
GitLab Runner is used to run your project's CI jobs and send the results back to GitLab.
- https://docs.gitlab.com/runner/

### Git Runner Executor
GitLab Runner implements a number of executors that can be used to run your builds in different scenarios, a better way is to use Docker as it allows to have a clean build environment, with easy dependency management (all dependencies for building the project could be put in the Docker image). The Docker executor allows you to easily create a build environment with dependent services, like MySQL.

