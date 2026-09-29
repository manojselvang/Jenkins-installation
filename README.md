# Jenkins-installation

Setup Jenkins On Kubernetes
For setting up a Jenkins Cluster on Kubernetes, we will do the following:

Create a Namespace

Create a service account with Kubernetes admin permissions.

Create local persistent volume for persistent Jenkins data on Pod restarts.

Create a deployment YAML and deploy it.

Create a service YAML and deploy it.



Jenkins Kubernetes Manifest Files
All the Jenkins Kubernetes manifest files used here are hosted on GitHub. Please clone the repository if you have trouble copying the manifest from the document.

`git clone https://github.com/scriptcamp/kubernetes-jenkins`

Use the GitHub files for reference and follow the steps in the next sections.

Kubernetes Jenkins Deployment
Let’s get started with deploying Jenkins on Kubernetes.

Step 1: Create a Namespace for Jenkins. It is good to categorize all the DevOps tools as a separate namespace from other applications.

`kubectl create namespace devops-tools`

Step 2: Create a 'jenkins-01-serviceAccount.yaml' file and copy the following admin service account manifest.

