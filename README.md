[![Apprenticeship-action](https://github.com/melippmann/LiatrioApp/actions/workflows/apprenticeship-action.yml/badge.svg)](https://github.com/melippmann/LiatrioApp/actions/workflows/apprenticeship-action.yml)

[![build and deploy to cloud run](https://github.com/melippmann/LiatrioApp/actions/workflows/deploy.yml/badge.svg)](https://github.com/melippmann/LiatrioApp/actions/workflows/deploy.yml)

# Liatrio Apprenticeship Interview Exercise
<details><summary>Description</summary><p>

This Repository is part of the Liatrio Apprenticeship Interview Exercise.

This document is being used to document how I approached the task.

</p>
</details>

## GitHub Repository
<details><summary>Task Description</summary><p>

- [x] Create a public GitHub Repository to store the code and files for the webApp.
- [x] Share the repo on Slack and push up changes frequently.

</p>
</details>

<details><summary>Setup details</summary><p>

  The following steps were taken to set up Git and GitHub:
  Create new dirrectory
  ```
  mkdir LiatrioApp
  ```
  Show directory was created
  ```
  ls
  ``` 
  navigate to the directory
  ```
  cd LiatrioApp
  ```
  initialize git tracking
  ```
  git init
  ```
  log into GitHub, create new repository, set to public, add README.md
  
  Connect local repo to Github repo
  
  ```  
    git remote add origin https://github.com/melippmann/LiatrioApp.git
    git remote show origin
    git remote -v
 ```   
  Want to track upstream as well:
```
  git remote add upstream https://github.com/melippmann/LiatrioApp.git
  git remote -v
  git pull origin main
  ls
  git push -u origin main
  ```
  Edit .md file and make first commit:
  ```
  git add README.md
  git commit -m "Updating markdown file with steps taken to set up git and GitHub for the application"
  git push origin main
```
My authentication failed as my personal access tokens are expired. Walking through creating new access tokens,
```
gh auth status
github.com
  X github.com: authentication failed
  - The github.com token in /home/meher/snap/gh/502/.config/gh/hosts.yml is no longer valid.
  - To re-authenticate, run: gh auth login -h github.com
  - To forget about this host, run: gh auth logout -h github.com

```
read the docs at: 

https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github

https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories

https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens

running the suggested command:

```
 gh auth login -h github.com
? What is your preferred protocol for Git operations? HTTPS
? Authenticate Git with your GitHub credentials? Yes
? How would you like to authenticate GitHub CLI? Login with a web browser

! First copy your one-time code: xxxx-xxxx
Press Enter to open github.com in your browser... 
✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
✓ Logged in as melippmann
```
Since I will want to set up GitHub actions late will want to review: 

https://docs.github.com/en/actions/security-guides/automatic-token-authentication

```
git push --set-upstream origin main
```
Share GitHub repo in Slack and push changes frequently.

</p>
</details>

## Node.js Application

<details><summary>requirements and processes</summary><p>
Install Node.js and use Express.js to build a simple single endpoint web applicaiton that returns the following JSON object.:

```
{
    "message": "My name is Meher Lippmann",
    "timestamp": dynamically genearted timestamp
}
```
Having never used Node.js or Express.js

The first thing I will do is peruse 
https://nodejs.org/en/about
and
https://expressjs.com/

I am running on Ubuntu 20.04; will install using apt:

```
sudo apt update
sudo apt install nodejs
node -v

```
```
v12.22.9
```
```
sudo apt install npm
```

I can now install Express.js as described: 

https://expressjs.com/en/starter/installing.html

In the LiatrioApp directory run:

```
npm init
```
This command is used to generate a package.json file for the project
```
package name: (liatrioapp) 
version: (1.0.0) 
description: This is a simple single endpoint web application that returns a JSON object with a message and dynamically set timestamp.
entry point: (index.js)
...
```
Default settings were choosen, though a description and authorship was added.

https://expressjs.com/en/starter/installing.html
```

npm install express
```
and following the "hello world" 
https://expressjs.com/en/starter/hello-world.html
turorial was enough to get the desired app up and running.

</p>
</details>

## Docker Containerization

<details><summary>process</summary><p>
using Docker's docs for node.js applications:
https://docs.docker.com/language/nodejs/containerize/

giving docker-desktop a try:
https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

following
https://docs.docker.com/desktop/install/ubuntu/

```
sudo apt install gnome-terminal
sudo apt-get update
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
Download the latest DEB package and install:

```
sudo apt-get update
sudo apt-get install ./docker-desktop-<version>-<arch>.deb

```
Now we can use 

```
docker init
Welcome to the Docker Init CLI!

This utility will walk you through creating the following files with sensible defaults for your project:
  - .dockerignore
  - Dockerfile
  - compose.yaml

Let's get started!

? What application platform does your project use? Node
? What version of Node do you want to use? 12.22.9
? Which package manager do you want to use? npm
? What command do you want to use to start the app: node app.js
? What port does your server listen on? 80

```
this creates

```
├── docker-nodejs-sample/
│ ├── spec/
│ ├── src/
│ ├── .dockerignore
│ ├── .gitignore
│ ├── compose.yaml
│ ├── Dockerfile
│ ├── package-lock.json
│ ├── package.json
│ └── README.md
```

run with 

```
docker compose up --build
```
navigating to
```
http://localhost:80/
``` 
in the browser demonstrates that it is working
```
ctr+c
```
to shut down.

To run in the background:
```
docker compose up --build -d

```
and to shut down:

```
docker compose down
```

</p>
</details>

## GitHub Actions

<details><summary>details</summary><p>

https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions

For the github action instead of using docker compose up/down

using 

```
docker build -t <tag-name>
docker run -dp 80:80 <tag-name>

```
The `-t` option in the `build` command is to designate a human readable tag name for the container
`-dp` is an option to run  in the background and port mapping `host:container`
https://docs.docker.com/get-started/02_our_app/


add notes on: 
https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions

# Push to dockerhub

https://medium.com/platformer-blog/lets-publish-a-docker-image-to-docker-hub-using-a-github-action-f0b17e5cceb3
https://medium.com/@deepakshakya/beginners-guide-to-use-docker-build-run-push-and-pull-4a132c094d75

</p>
</details>

## Cloud Deployment

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

<details><summary>details</summary><p>

https://github.com/google-github-actions/deploy-cloudrun

Configure workload identity federation with deployment pipelines for GitHub
https://cloud.google.com/iam/docs/workload-identity-federation-with-deployment-pipelines



</p>
</details>