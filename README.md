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

The 'jenkins-01-serviceAccount.yaml' creates a 'jenkins-admin' clusterRole, 'jenkins-admin' ServiceAccount and binds the 'clusterRole' to the service account.

The 'jenkins-admin' cluster role has all the permissions to manage the cluster components. You can also restrict access by specifying individual resource actions.

Now create the service account using kubectl.

`kubectl apply -f jenkins-01-serviceAccount.yaml`

Step 3: Create 'jenkins-02-volume.yaml' and copy the following persistent volume manifest.

Important Note: Replace 'worker-node01' with any one of your cluster worker nodes hostname.

You can get the worker node hostname using the kubectl.

`kubectl get nodes`

For volume, we are using the 'local' storage class for the purpose of demonstration. Meaning, it creates a 'PersistentVolume' volume in a specific node under the '/mnt' location.

As the 'local' storage class requires the node selector, you need to specify the worker node name correctly for the Jenkins pod to get scheduled in the specific node.

If the pod gets deleted or restarted, the data will get persisted in the node volume. However, if the node gets deleted, you will lose all the data.

Ideally, you should use a persistent volume using the available storage class with the cloud provider, or the one provided by the cluster administrator to persist data on node failures.

Let’s create the volume using kubectl

`kubectl create -f jenkins-02-volume.yaml`

Step 4: Create a Deployment file named 'jenkins-03-deployment.yaml' and copy the following deployment manifest.

