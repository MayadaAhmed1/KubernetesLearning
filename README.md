# KubernetesLearning
- **Project Overview**
- **Project Structure**
- **Deploy Docker App using Kubernetes**

📌 **Project Overview** simple web application node.js has two endpoints:

 Get request to nothing , Get request to error

 Our target to deploy the project to kubernetes cluster 

📂 **Project Structure**

│── KubernetesLearning/

`├── kub-action-01-starting-setup 
 ├── dockerfile                        # Docker configuration
 ├── .dockerignore                     # Files to be ignored
 ├── package.json                      # Dependencies
 ├── app.js                            # Application source code  
 ├── images                            # Readme images 
├── README.md                          # Project details`

# **Deploy Docker App using Kubernetes**

 Pre requisite:

Download kubctl (is the **command-line tool** used to interact with **Kubernetes clusters)**

`brew install kubectl`

install minikube (**Lightweight Kubernetes cluster** that runs locally on your machine)

`brew install minikube`

Start a cluster using the parallels driver: (If you're using the **standard edition**, it **does not support CLI** for VMs ),check driver based on your machine type 
https://minikube.sigs.k8s.io/docs/drivers/

```jsx
minikube start --driver=parallels
```

Start a cluster using the driver by checking the compatible driver based on your machine type 
https://minikube.sigs.k8s.io/docs/drivers/

```
minikube start --driver=docker
```

install minikube dashboard to bring visual view for clusters

`minikube dashboard` 

Deployment Steps:

Build docker image 

`docker build -t kub-firts-app .`

`docker build -t image_Name .`

Create repo at dockerHub with name “`Hub_image_Name` ” ,then push the image 

`docker tag kub-first-app mayadaabdelsalam/kub-first-app` 

`docker push mayadaabdelsalam/kub-first-app`

`docker tag image_Name Hub_image_Name` 

`docker push Hub_image_Name` 

Then we send the build image to kubernetes cluster as part of deployment which offer container running in the pod 

`kubectl create deployment DeploymentName  -—image=Hub_image_Name`

`kubectl create deployment first-app --image=mayadaabdelsalam/kub-first-app` 

to check deployments status

`kubectl get deployment`

to get pods status 

`kubectl get pods`

to check dashboard 

 `minikube dashboard`

![Screenshot 2025-03-20 at 19.26.43.png](attachment:b2a145e3-9c12-46c8-a9b6-1709f99610c6:Screenshot_2025-03-20_at_19.26.43.png)

Assign specific port to the cluster so we can access the app

 `kubectl expose deployment first-app --type=LoadBalancer --port=8080`

To view your node.js application running in the container 

 `minikube service first-app`

![Screenshot 2025-03-20 at 19.40.01.png](attachment:8e68c853-6f0b-4ecc-9e1a-c21715c413cc:Screenshot_2025-03-20_at_19.40.01.png)

Scale the Pod/container 

`kubectl scale deployment/first-app --replicas=3`

Summery for docker and kubernetes deployment steps

![Screenshot 2025-03-21 at 10.11.27.png](attachment:8116e391-4d0f-4eb3-9e71-5ec8f7402f99:Screenshot_2025-03-21_at_10.11.27.png)

🌟 **Contributing**

This is a personal learning project, but feel free to open an issue or suggest improvements.

**useful links:**

https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/

https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Farm64%2Fstable%2Fhomebrew
https://minikube.sigs.k8s.io/docs/drivers/
