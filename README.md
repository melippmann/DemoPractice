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

</p></details>
<details><summary>Read the Docs</summary><p>

https://docs.github.com/en/actions

https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions
  
https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions

</p></details>

<details><summary>Walkthrough</summary><p>
</p></details>
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
In git, pull the changes from the repo to sync and then add, commit and push all the application files up to GitHub:

```
git pull

```
Now we can commit our changes and push to the github repo


## Cloud Deployment
<details><summary>Task</summary><p>

</p></details>
<details><summary>Tool Description</summary><p>

</p></details>
<details><summary>Read the Docs</summary><p>

</p></details>

<details><summary>Walkthrough</summary><p>
</p></details>

<details><summary>details</summary><p>
<!-- 
## Create new project
left panel: VM instances
## create instance
  name: instance-1
  region: us-west1 (oregon)
  zone: us-west1-b
  Machine configuration: E2
  Machine type: shared-core e2-micro
  availability: standard
## Container
  # deploy container
    container image: melippmann / liatrio_apprenticeship_exercise
  # boot disk
    versopm: container-optimized OS 
    boot disk type: standard persistent disk
    size: 10 (GB)
## Identity and API access
  Compute Engine default service account
## Access scopes
  Allow default access
## Firewall
  allow HTTP trafic -->

## Using Google Cloud Run:

 deploy one revision from an existing conterin image
 container image URL: docker.io/melippmann/liatrio_apprenticeship_exercise
 service name: liatrio-apprenticeship-exercise
 region: us-west1 (Oregon)
 CPU is only allocated during request processing
 maximum number of instances: 4
 Ingress control: All
 Authentication: Allow unauthenticated invocations
 create
</p>
</details>

## Deployment Workflow
<details><summary>Task</summary><p>

</p></details>
<details><summary>Tool Description</summary><p>

</p></details>
<details><summary>Read the Docs</summary><p>

</p></details>

<details><summary>Walkthrough</summary><p>
</p></details>

<details><summary>details</summary><p>

https://github.com/google-github-actions/deploy-cloudrun

Configure workload identity federation with deployment pipelines for GitHub
https://cloud.google.com/iam/docs/workload-identity-federation-with-deployment-pipelines



</p>
</details>