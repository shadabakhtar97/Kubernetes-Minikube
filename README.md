# Kubernetes-Minikube
Learn Kubernetes for Development Environment with Minikube Deep Dive
### Kubernetes-Minikube All Commands in One Go
Download Minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
Install Minikube
```
curl install minikube-linux-amd64 /usr/local/bin/minikube
```
Download "kubect"
```
curl -o kubectl https://storage.googleapis.com/kubernetes-release/release/v1.23.3/bin/linux/amd64/kubectl
```
Change User Permission
```
chmod u+x kubectl
```
Move "kubectl" to /usr/local/bin
```
sudo mv kubectl /usr/local/bin
```
Check "kubectl" Version
```
kubectl version --short
```
Start/Stop/Status Minikube with Single Node(Control Plane Node)
```
minikube start/stop/status
```
Start/Stop/Status Minikube with Multi Node(Control Plane Node and Worker Node)
```
Check All Default Pods
```
minikube kubectl -- get pods -A
```
minikube start --nodes 3 -p shadabcluster
```
Check All Nodes
```
kubectl get nodes
```



### What is Minikube ?
Minikube is an open-source tool that facilitates the local deployment of a single-node Kubernetes cluster on your development machine. Kubernetes is a powerful container orchestration platform used for managing containerized applications. Minikube makes it easier for developers to test and develop applications in a Kubernetes environment without the need for a full-scale, multi-node Kubernetes cluster.

### Key features of Minikube include:
1. Local Kubernetes Cluster: Minikube allows you to run a minimal, single-node Kubernetes cluster on your local machine. This helps you simulate a Kubernetes environment for development and testing purposes.

2. Isolation: It provides isolation for your local Kubernetes cluster, so it won't interfere with any existing Kubernetes clusters you might be using.

3. Easy Setup: Minikube is relatively easy to set up and use. It can be installed on various operating systems, including Windows, macOS, and Linux.

4. Multiple Hypervisors: Minikube supports multiple hypervisors, such as VirtualBox, VMware, KVM, and others, allowing you to choose the one that best fits your development environment.

5. Add-Ons: Minikube comes with a range of add-ons that enable additional functionality, such as the Kubernetes Dashboard for visual management, the Metrics Server for resource monitoring, and others.

6. CLI Interface: It offers a command-line interface (CLI) for starting, stopping, and managing the local Kubernetes cluster.

Minikube is particularly useful for developers who want to learn and experiment with Kubernetes, test applications in a Kubernetes environment, or develop and debug Kubernetes resources without the overhead of managing a full-scale Kubernetes cluster. It is not intended for production use, as it only provides a single-node cluster, whereas production environments typically involve multi-node clusters for scalability and high availability.
### --------------------------------------------------------------------------------------------------
### Pre-requisites for Minikube for Ubuntu VM in AWS ?
To set up Minikube on an Ubuntu virtual machine (VM) in AWS, you'll need to ensure that your VM meets certain prerequisites and follow these steps:

**Prerequisites:**

1. **Ubuntu VM**: You should have an Ubuntu virtual machine running on AWS. Make sure it's up to date with the latest packages and security updates. You can use an official Ubuntu Amazon Machine Image (AMI) to launch your VM.

2. **Hypervisor**: Minikube uses a hypervisor to create a virtual machine for your local Kubernetes cluster. You can choose from several options, including VirtualBox, VMware, KVM, or others. You'll need to have your chosen hypervisor installed on your Ubuntu VM.

3. **Docker**: Minikube typically uses Docker as its container runtime. You should have Docker installed on your Ubuntu VM. You can install it using the following commands:

   ```shell
   sudo apt update
   sudo apt install docker.io
   sudo systemctl enable docker
   sudo systemctl start docker
   ```

4. **Kubectl**: You'll need the `kubectl` command-line tool to interact with your Kubernetes cluster. You can install it using the following commands:

   ```shell
   sudo apt update
   sudo apt install kubectl
   ```

5. **Minikube**: You'll also need to install Minikube itself. Here's how you can do it:

   - Download the Minikube binary:

     ```shell
     curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
     ```

   - Make the Minikube binary executable:

     ```shell
     chmod +x minikube-linux-amd64
     ```

   - Move the Minikube binary to a directory in your system's PATH (e.g., /usr/local/bin):

     ```shell
     sudo mv minikube-linux-amd64 /usr/local/bin/minikube
     ```

6. **Start Minikube**: Once you have Minikube installed, you can start your local Kubernetes cluster by running:

   ```shell
   minikube start --driver=<hypervisor>
   ```

   Replace `<hypervisor>` with the name of the hypervisor you've installed (e.g., "virtualbox," "vmware," "kvm2," etc.).

7. **Verification**: After starting Minikube, you can verify the cluster's status using the following command:

   ```shell
   minikube status
   ```
### --------------------------------------------------------------------------------------------------
### What are the command commands use for minikube ?
Minikube provides a command-line interface (CLI) that allows you to manage and interact with your local Kubernetes cluster. Here are some of the most commonly used Minikube commands:

1. **Start Minikube:**
   To start your Minikube cluster, you can use the following command:
   ```
   minikube start
   ```
   You can also specify a specific hypervisor if Minikube doesn't automatically detect it, for example:
   ```
   minikube start --driver=<hypervisor>
   ```

2. **Stop Minikube:**
   To stop your Minikube cluster when you're done working with it, use:
   ```
   minikube stop
   ```

3. **Delete Minikube:**
   To delete the Minikube cluster and clean up all associated resources, use:
   ```
   minikube delete
   ```

4. **View Minikube Status:**
   You can check the status of your Minikube cluster with:
   ```
   minikube status
   ```

5. **Dashboard:**
   Minikube provides a dashboard for managing your cluster. To open the Kubernetes dashboard, you can use the following command:
   ```
   minikube dashboard
   ```

6. **SSH into Minikube:**
   You can SSH into the Minikube VM to perform debugging or access the Kubernetes nodes:
   ```
   minikube ssh
   ```

7. **Enable Add-Ons:**
   Minikube supports various add-ons, such as the Kubernetes Dashboard and Metrics Server. You can enable these add-ons using the `minikube addons` command. For example:
   ```
   minikube addons enable dashboard
   ```

8. **Tunnel:**
   To access services running in your cluster, you can set up a tunnel with the following command:
   ```
   minikube tunnel
   ```

9. **Profile Management:**
   If you have multiple Minikube profiles, you can switch between them using the `profile` subcommand. For example:
   ```
   minikube profile list
   minikube profile <profile-name>
   ```

10. **Version Information:**
    To check the Minikube version, use:
    ```
    minikube version
    ```

11. **Additional Commands:**
    Minikube offers several other commands and options for advanced configuration and management, such as specifying CPU and memory allocations, configuring the Kubernetes version, and more. You can explore these commands by running `minikube --help` or `minikube <command> --help` for specific command options.

### --------------------------------------------------------------------------------------------------
### What are common commands for Minikube multi node cluster?
Minikube is primarily designed to create single-node Kubernetes clusters for local development and testing. If you need a multi-node Kubernetes cluster, you would typically use a different tool or a cloud-based Kubernetes service such as AWS EKS, Google Kubernetes Engine (GKE), or Azure Kubernetes Service (AKS).

However, if you're interested in creating a multi-node Kubernetes cluster for testing or experimentation using Minikube, you can set up multiple Minikube instances and configure them to communicate with each other. Here's a high-level overview of the process, along with some common commands you might use:

1. **Install Multiple Minikube Instances:**
   First, you need to install and start multiple Minikube instances, each representing a separate node in your cluster. You can do this by specifying different profiles for each Minikube instance. For example:
   ```
   minikube start -p node1
   minikube start -p node2
   ```

2. **Get the Cluster Configuration:**
   To interact with the cluster, you can get the configuration for each Minikube profile using the `minikube profile` command:
   ```
   minikube profile node1
   minikube profile node2
   ```

3. **Set the Current Cluster Context:**
   You can switch between the cluster contexts using the `kubectl config` command, specifying the profile name. For example, to switch to the "node1" cluster:
   ```
   kubectl config use-context node1
   ```

4. **Deploy Applications:**
   You can use `kubectl` to deploy your applications to the respective Minikube instances. Be sure to specify the correct context for the cluster you want to deploy to.

5. **Interconnect the Nodes:**
   To create a multi-node cluster, you would need to configure the nodes to communicate with each other. This typically involves setting up network routing and ensuring that the nodes can reach each other's services. The exact steps for this can be complex and would depend on your specific environment and requirements.
### --------------------------------------------------------------------------------------------------
### Minikube --help
However, you can run `minikube --help` in your terminal to get a list of available Minikube commands and options. Here's an example of what you might see when running `minikube --help`:

```plaintext
Minikube is a CLI tool that provisions and manages single-node Kubernetes clusters
optimized for development workflows.

Usage:
  minikube [command]

Available Commands:
  addons       Modify minikube's kubernetes addons
  cache        Add or delete an image from the local cache.
  config       Modify persistent configuration values
  dashboard    Access the kubernetes dashboard running within the minikube cluster
  delete       Deletes a local k8s cluster
  docker-env   Configure environment to use minikube's Docker daemon
  ip           Retrieves the IP address of the running cluster
  kubectl      Run kubectl
  logs         Retrieves the logs of the primary node and saves it to a location
  mount        Mounts the specified directory into minikube
  profile      Get or set the current profile
  service      Gets the URL of the service with the given name
  ssh          Log into or run a command on a machine with SSH; very useful for debugging clusters
  ssh-key      Retrieve the ssh identity key path of the specified cluster
  start        Starts a local k8s cluster
  status       Gets the status of a local k8s cluster
  stop         Stops a running local k8s cluster
  update-check Print current and latest version number
  update-context Verify the IP address of the running cluster in kubeconfig.
  tunnel       Create a route to services deployed in minikube
  version      Print the version of minikube

Flags:
  -h, --help   help for minikube


### Minikube Kubectl commands


Use "minikube [command] --help" for more information about a command.
```

You can run specific commands with `minikube <command>` to access more detailed information and options for each command. For instance, to get help for the `start` command, you can run `minikube start --help`.
### --------------------------------------------------------------------------------------------------
### Minikube Kubectl commands
Minikube uses `kubectl` (Kubernetes command-line tool) to interact with the Kubernetes cluster running in your Minikube environment. The commands you use with `kubectl` in the context of Minikube are the same as those used with any Kubernetes cluster. Here are some common `kubectl` commands and their usage within Minikube:

1. **View Cluster Information:**

   - `kubectl cluster-info`: View information about the Kubernetes cluster running in Minikube.
   - `kubectl version`: Check the client and server Kubernetes versions.

2. **Managing Resources:**

   - `kubectl get pods`: List all pods in the cluster.
   - `kubectl get services`: List all services in the cluster.
   - `kubectl get deployments`: List all deployments in the cluster.
   - `kubectl get nodes`: List all nodes in the cluster.

3. **Creating and Managing Resources:**

   - `kubectl create deployment <name> --image=<image>`: Create a deployment.
   - `kubectl expose deployment <name> --type=NodePort --port=<port>`: Expose a deployment as a service with a NodePort.
   - `kubectl apply -f <yaml-file>`: Apply a configuration file to create resources (e.g., pods, services).
   - `kubectl delete deployment <name>`: Delete a deployment and its associated resources.

4. **Accessing Applications:**

   - `kubectl port-forward <pod-name> <local-port>:<pod-port>`: Forward a port from your local machine to a pod.
   - `minikube service <service-name>`: Open a service in a web browser.

5. **Scaling Resources:**

   - `kubectl scale deployment <name> --replicas=<replica-count>`: Scale the number of replicas in a deployment.

6. **Viewing Logs and Debugging:**

   - `kubectl logs <pod-name>`: View the logs of a specific pod.
   - `kubectl exec -it <pod-name> -- /bin/sh`: Get an interactive shell inside a pod for debugging.

7. **Updating Resources:**

   - `kubectl set image deployment/<name> <container-name>=<new-image>`: Update the image of a container in a deployment.

8. **Labeling and Annotating Resources:**

   - `kubectl label pods <pod-name> <label-key>=<label-value>`: Add labels to pods.
   - `kubectl annotate pods <pod-name> <annotation-key>=<annotation-value>`: Add annotations to pods.

9. **Configuring the Current Context:**

   - `kubectl config use-context minikube`: Set the current context to the Minikube cluster.

10. **Resource Descriptions:**

    - `kubectl describe <resource> <resource-name>`: Display detailed information about a specific resource.

These are some of the common `kubectl` commands that you can use to manage and interact with the Kubernetes cluster running in Minikube. You can also use `kubectl --help` to get more information about specific `kubectl` commands and their options.
### --------------------------------------------------------------------------------------------------
### How to run python login page by minikube?
To run a Python login page within a Kubernetes cluster created by Minikube, you need to create a set of Kubernetes resources, including pods, services, and possibly persistent storage. Here's a step-by-step guide to set up a simple Python login page application within Minikube:

1. **Create a Python Application**:

   First, create a simple Python login page application. You can use a web framework like Flask or Django to build your application. Ensure that your Python application provides a login page with the necessary functionality.

2. **Dockerize Your Python Application**:

   Containerize your Python application using Docker. Write a Dockerfile that specifies how to build the container image. Here's a simplified example for a Flask app:

   ```Dockerfile
   FROM python:3.9

   WORKDIR /app
   COPY . /app

   RUN pip install -r requirements.txt

   CMD ["python", "app.py"]
   ```

3. **Build and Push the Docker Image**:

   Build your Docker image and push it to a container registry, such as Docker Hub, or use the Minikube Docker daemon. If you're using the Minikube Docker daemon, you can build and tag the image with the Minikube environment's Docker host IP:

   ```shell
   eval $(minikube docker-env)
   docker build -t your-image-name:your-tag .
   ```

4. **Create Kubernetes Resources**:

   Now, create Kubernetes resources to deploy your Python application. Create a Kubernetes Deployment and a Service to expose your application. Here's a simplified example of Kubernetes YAML files:

   `deployment.yaml`:

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: python-login-app
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: python-login-app
       spec:
         containers:
         - name: python-login-container
           image: your-image-name:your-tag
           ports:
           - containerPort: 80
   ```

   `service.yaml`:

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: python-login-service
   spec:
     selector:
       app: python-login-app
     ports:
     - protocol: TCP
       port: 80
       targetPort: 80
     type: NodePort
   ```

5. **Apply the Kubernetes Resources**:

   Apply the Kubernetes resource definitions to create and run your Python login application:

   ```shell
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

6. **Access Your Application**:

   Retrieve the NodePort assigned to your service:

   ```shell
   kubectl get svc python-login-service
   ```

   You should see a NodePort that you can use to access your Python login page. Access it through your Minikube IP:

   ```
   http://<minikube-ip>:<node-port>
   ```

   You can get your Minikube IP using:

   ```shell
   minikube ip
   ```
   ### --------------------------------------------------------------------------------------------------

### Kubernetes with Python Applications
### Kubernetes Project1 Documentation

**Table of Contents:**
1. Introduction
2. Prerequisites
3. Docker and Minikube Setup
4. Creating a Python Application
5. Creating Kubernetes Resources
6. Deployment Issue and Solution
7. Server Storage Upgrade
8. Renaming the Python Application

**1. Introduction:**
   - Provide an overview of the project.
   - Explain the goal of deploying a Python application with Kubernetes.

**2. Prerequisites:**
   - Ensure you have Docker and Minikube installed.
     ```
     $ sudo service docker status
     ● docker.service - Docker Application Container Engine
     ...
     ...
     $ minikube start -p multinode-shadab
     $ minikube status -p multinode-shadab
     ...
     ```

**3. Docker and Minikube Setup:**
   - Explain how to set up Docker and Minikube.
     ```
     $ sudo service docker status
     ...
     ...
     $ minikube start -p multinode-shadab
     $ minikube status -p multinode-shadab
     ...
     ```

**4. Creating a Python Application:**
   - Provide instructions on creating a Python application.
     - Create a Python source file (k8s-python-app.py).
     ```
     $ touch k8s-python-app.py
     $ vim k8s-python-app.py
     # Insert Python code
     ```

   - Create a Dockerfile to build the Docker image.
     ```
     $ touch Dockerfile
     $ vim Dockerfile
     # Use an official Python runtime as a parent image
     FROM python:3.8-slim
     WORKDIR /app
     COPY . /app
     CMD ["python3", "k8s-python-app.py"]
     ```

   - Build the Docker image.
     ```
     $ sudo docker build -t k8s-python-app:v1 .
     ```

**5. Creating Kubernetes Resources:**
   - Explain the steps to create Kubernetes resources, including Deployment and Service.
     - Provide sample YAML files for Deployment (deployment.yaml) and Service (service.yaml).
     - Mention the issue of missing "selector" when applying Kubernetes resources and the solution.
     ```
     deployment.yaml:
     
apiVersion: apps/v1
kind: Deployment
metadata:
  name: k8s-python-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: k8s-python-app
  template:
    metadata:
      labels:
        app: k8s-python-app
    spec:
      containers:
      - name: k8s-python-app-container
        image: k8s-python-app:v1
        ports:
        - containerPort: 80

     service.yaml:
     
     apiVersion: v1
     kind: Service
     metadata:
       name: k8s-python-app-service
     spec:
       selector:
         app: k8s-python-app
       ports:
       - protocol: TCP
         port: 80
         targetPort: 80
       type: NodePort
     ```

**6. Deployment Issue and Solution:**
   - Describe the issue of missing "selector" during the deployment.
     ```
     $ kubectl apply -f deployment.yaml
     error: error validating "deployment.yaml": error validating data: ValidationError(Deployment.spec): missing required field "selector" in 
     io.k8s.api.apps.v1.DeploymentSpec; if you choose to ignore these errors, turn validation off with --validate=false
     ```

   - Explain the solution, which involves removing deployment.yaml from /var/tmp.
     ```
     $ kubectl apply -f deployment.yaml --validate=false
     The Deployment "k8s-python-app" is invalid:
     * spec.selector: Required value
     * spec.template.metadata.labels: Invalid value: map[string]string{"app":"k8s-python-app"}: `selector` does not match template `labels`
     
     Solution:
     Need to remove deployment.yaml from /var/tmp
     ```

**7. Server Storage Upgrade:**
   - Describe the need for server storage upgrade.
   - Mention options like creating backups and snapshots.

**8. Renaming the Python Application:**
   - Explain how to rename the Python application from app.py to k8s-python-app.py.
     ```
     $ sudo mv app.py k8s-python-app.py
     ```

** Issue: **

   ```
$ kubectl apply -f deployment.yaml
   ```
error: error validating "deployment.yaml": error validating data: ValidationError(Deployment.spec): missing required field "selector" in io.k8s.api.apps.v1.DeploymentSpec; if you choose to ignore these errors, turn validation off with --validate=false

   ```

apiVersion: apps/v1
kind: Deployment
metadata:
  name: k8s-python-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: k8s-python-app
  template:
    metadata:
      labels:
        app: k8s-python-app
    spec:
      containers:
      - name: k8s-python-app-container
        image: k8s-python-app:v1
        ports:
        - containerPort: 80

   ```






