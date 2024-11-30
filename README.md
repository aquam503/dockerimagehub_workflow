## This project demonstrates how to work with GitHub Actions by implementing CI/CD workflows and leveraging Docker Hub for container management.

This repository contains a GitHub Actions workflow that automates tasks for a Flask application using Docker. It ensures the application is tested, built, and deployed automatically whenever changes are made to the code.

How It Works
The workflow is triggered when:

Code is pushed to the main branch.
A pull request is opened for the main branch.
Steps in the Workflow
1. Workflow Events
on:  
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

push: Runs the workflow when you push code to the main branch.
pull_request: Runs the workflow when someone creates a pull request targeting the main branch.

2. Jobs
The workflow is divided into three jobs:

dockerbuild
build-and-test
build-and-publish

* Job 1: Build Docker Image

Purpose: Builds a Docker image for the application.
Steps:
Checkout the code: Downloads the repository code.
Build the Docker image:
docker build .: Builds the image using the DockerFile.
--tag: Tags the image with a unique name, including the current timestamp.

* Job 2: Build and Test

Purpose: Verifies the code works correctly by running tests.
Steps:
Checkout the code: Same as in Job 1.
Set up Python: Installs Python version 3.9 for testing.
Install dependencies: Installs required Python packages from requirements.txt.
Run tests: Executes tests using pytest to verify application functionality.

* Job 3: Build and Publish Docker Image

Purpose: Publishes the Docker image to DockerHub.
Steps:
1. Checkout the code: Same as before.
2. Set up Docker Buildx: Prepares for advanced Docker builds.
3. Login to DockerHub:
DOCKER_USERNAME and DOCKER_PASSWORD are securely stored as GitHub secrets.
4. Build and push the Docker image:
Builds the image using the DockerFile.
Pushes the image to DockerHub with the tag latest.
5. Output the image digest: Prints a unique identifier for the pushed image.




This workflow simplifies the development process by automating testing, building, and deploying the Flask application, saving time and reducing manual errors.