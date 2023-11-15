# Liatrio Apprenticeship Interview Exercise

  <details><summary>Description</summary><p>

    This demo will showcase how to stand-up a Node.js applicaiton in a Docker container and both build and deploy the applicaiton to Google Cloud using Github Actions.
  </p></details>

## GitHub Repository

<details><summary>Task</summary><p>

- [] Create a public GitHub Repository to store the code and files for the webApp.
- [] This Repo will also be used to host a Github Actions workflow.
</p></details>

<details><summary>Tool description</summary><p>

>Git...is a distributed version control system that tracks changes in any set of computer files.

>GitHub...is a platform and cloud-based service for software development and version control using Git, allowing developers to store and manage their code. It provides the distributed version control of Git plus access control, bug tracking, software feature requests, task management, continuous integration, and wikis for every project.
  
</p></details>


<details><summary>Read the Docs</summary><p>

https://docs.github.com/en/get-started/quickstart/create-a-repo
</p>
</details>

<details><summary>Walkthrough</summary><p>
  
  - [] initialize git tracking in the project directory
  ```
  git init
  ```

  - [] log into GitHub, create a new repository, and add .gitignore file
  
  - [] Connect local repo to Github repo
  
  ```  
    git remote add origin https://github.com/melippmann/Demo
    git remote add upstream https://github.com/melippmann/Demo
    git pull origin main
    git add app.js Dockerfile Package.json package-lock.json README.md
    git commit -m "Add local app and Dockerfile to GitHub"
  ```
</p></details>

## Node.js Application

<details><summary>Task</summary><p>
Install Node.js and use Express.js to build a simple single endpoint web applicaiton that returns the following JSON object.:

```
{
    "message": "My name is   __________",
    "timestamp": 123456789
}
```
Where the typestamp is dynamically generated.
</p></details>

<details><summary>Tool description</summary><p>
  
  >As an asynchronous event-driven JavaScript runtime, Node.js is designed to build scalable network applications...users of Node.js are free from worries of dead-locking the process, since there are no locks. Almost no function in Node.js directly performs I/O, so the process never blocks except when the I/O is performed using synchronous methods of Node.js standard library. Because nothing blocks, scalable systems are very reasonable to develop in Node.js.

  >Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.
</p></details>

<details><summary>Read the Docs</summary><p>

https://nodejs.org/en/about

https://expressjs.com/

https://expressjs.com/en/starter/installing.html


https://expressjs.com/en/starter/hello-world.html
</p></details>

<details><summary>Walkthrough</summary><p>

I am running on Ubuntu 20.04; will install using apt:

```
sudo apt update
sudo apt install nodejs
sudo apt install npm
```
In the project directory run:

```
npm init
```

This command is used to generate package.json and package-lock.json files for the web app

```
package name: (liatrioapp) 
version: (1.0.0) 
description: This is a simple single endpoint web application that returns a JSON object with a message and dynamically set timestamp.
entry point: (app.js)
...
```
Default settings can be choosen.

Now we can install express.js
```
npm install express
```
Following a "hello world" example from the docs above is enough to build the desired app with minor modifications.

</p>
</details>

## Docker Containerization
<details><summary>Task</summary><p>
 
- [] Write a Dockerfile that will build and run the application

</p></details>
<details><summary>Tool Description</summary><p>
  
  >A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
</p></details>

<details><summary>Read the Docs</summary><p>

Docker's docs for node.js applications:

https://docs.docker.com/language/nodejs/containerize/

</p></details>

<details><summary>Walkthrough</summary><p>


```
  docker build . -t <tag-name>
  docker run -dp 80:8080 <tag-name>

```

Verify that the app is runingnavigate to the browser and enter:
```
http://localhost/80

```
To stop the container
```
docker ps
docker stop <container-id>
```

</p>
</details>

## GitHub Actions
<details><summary>Task</summary><p>
  
  - [] Create a GitHub Actions Workflow that will:
    - [] build the applications Docker Image
    - [] Verifiy the application functionality using the Liatrio GitHub [apprentice-action](https://github.com/liatrio/github-actions/tree/master/apprentice-action)
    - [] Pushes the image to Docker Hub

    This third party action will test 
    - [] the status code of the root endpoint
    - [] that a json object with a message is returned
    - [] that the message has a timestamp property
    - [] contains: "My name is"
    - [] time stamp is numeric

  The test uses a docker bridge on port 80 and the action requires a built container to run.

  In the workflow we can use the --publish flag for port mapping:


  ```
    -p host:container
  ```
</p></details>

<details><summary>Tool Description</summary><p>

  >GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD. Build, test, and deploy your code right from GitHub. Make code reviews, branch management, and issue triaging work the way you want.
</p></details>
<details><summary>Read the Docs</summary><p>

https://docs.github.com/en/actions

https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions
  
https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions

</p></details>

<details><summary>Walkthrough</summary><p>

Navigate to actions in the GitHub repo

[set up a workflow yourself](https://github.com/melippmann/DemoPractice/new/main?filename=.github%2Fworkflows%2Fmain.yml&workflow_template=blank)

We need to Create a dockerhub acount and create a repo:

https://hub.docker.com/

In githup navigate to 

[settings](https://github.com/melippmann/LiatrioApp/settings)
[Secrets and variables for actions](https://github.com/melippmann/LiatrioApp/settings/secrets/actions)

create new repository secrets for the DockerHub username and password used in the Action file

```
  ${{secrets.DOCKER_USER}}
  ${{secrets.DOCKER_PASSWORD}}

```
In git, pull the changes
```
git pull

```
Now we can commit our changes and push to the github repo

</p></details>

## Cloud Deployment

<details><summary>Task</summary><p>

- [] Deploy to Google Could Platform using image from Docker Hub
</p></details>
<details><summary>Tool Description</summary><p>
  
  >Fully managed platform for containerized applications...You can write code using your favorite language, framework, and libraries, package it up as a container, run `gcloud run deploy`, and your app will be live—provided with everything it needs to run in production...fast autoscaling...automatically build container images form source code...run scheduled jobs to completion...
</p></details>
<details><summary>Read the Docs</summary><p>

https://cloud.google.com/run/docs/deploying
</p></details>

<details><summary>Walkthrough</summary><p>

## Using Google Cloud Run:


  - [] sign into google cloud
  - [] create a new Project
    - [] Go to Cloud Run
    - [] create a new service
    - [] Deploy one revision from an existing container image (docker.io/melippmann/demo)
    - [] region: us-west1 (Oregon)
    - [] set max # instances
    - [] allow access
    - [] allow unauthenticated invocations
  
</p>
</details>

## Deployment Workflow
<details><summary>Task</summary><p>

  - []Add a GitHub Workflow to automatically deploy the applicaiton to the cloud platform when changes are made to the main branch of the repository


</p></details>
<details><summary>Tool Description</summary><p>

</p></details>
<details><summary>Read the Docs</summary><p>

https://github.com/google-github-actions/deploy-cloudrun

Configure workload identity federation with deployment pipelines for GitHub

https://cloud.google.com/iam/docs/workload-identity-federation-with-deployment-pipelines
</p></details>

<details><summary>Walkthrough</summary><p>
- [] create a new Project
    - [] set up Cloud Run
    - [] IAM & Admin
    - [] create Service Acount: demo-deploy
    - [] Grant Permisions to sevice acount
      - [] App Engine Admin
      - [] Cloud Build Service Account
      - [] Cloud Run Admin
      - [] Service Acount user
      - [] copy the service account email address and paste into deploy yaml
    - []  create Workload Identity Federation
      - [] Create workload Identity provider and pool
      - [] add a provider to pool
        - [] OpenId Connect (OIDC)
      - [] provider details
        - [] provider name and id can be the same
          - demo-deploy-pool
        - [] Issuer(url)
          - [] https://token.actions.githubusercontent.com/
      - [] copy the link to use in the deploy action
        - [] ex: projects/73280995160/locations/global/workloadIdentityPools/demo-deploy/providers/demo-deploy-pool
      - [] Configure Provider Attributes:
        - [] google.subject == assertion.sub
        - [] grant access to service account
</p>
</details>