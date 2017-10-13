# Single Container Loop 
In this chapter you will get a basic experience in working with containers. For this chapter we concentrate on single container applications running locally or in Azure Container Instances.

**TODOS**
- Snippet für Container Registry -> Credentials, Anlegen, Screenshot
- Snippet Docker auf Ubuntu installieren


## 1. Containerize your app 
- Get the sample code of our hello world application **here**. **TODO LINK MISSING**
- Create a container image locally
- Run the image in a container locally on your machine. Remember to open up a port in your command (-p).

## 2. Automate your build 
- Import the sample code from to your VSTS Team Project. You can do this via UI. **TODO**
- Use VSTS to create a build definition which triggers on code changes. The build definition should 
    - create a new container image 
    - **TODO NPM**
    - use the build number as tag to identify your image. The buildnumber can be found in variable *$(Build.BuildNumber)* 
    - push the new image to your private Azure Container Registry (if you don't have an ACR, create one first)

## 3. Release to ACI manually
- Run your newly created image in Azure Container Instances to see if everything works. You can start it manually in the portal or via command line.


## 4. Relase to ACI via VSTS
- Use VSTS to create a release definition which is triggered by your build definition. This release definition should
    - deploy the latest image created by your build definition to ACI. Use the Azure CLI 
    task.
- Now you have a full end to end flow for single container applications.




# Kubernetes 101 
In this chapter you will set up a Kubernetes cluster in Azure Container Services (ACS) and an Azure Container Registry (ACR) to store your images.
**TODO Install Kubectl **
## 1. Create a Kubernetes cluster on Azure Container Services 
- Follow the instructions found here to set up your cluster **TODO LINK MISSING**
The deployment will take some time (~20 min). 

## 1. Run single container app in your K8s cluster
- Run a public available application in a single container on your cluster. The image name is "nginx".
**TODO: run befehl mit angeben** 
- Add a service to make your application accessible from the internet
**TODO: beschreibung & commands service anlegen**
**Beschreibung LB**
- Start your webbrowser to view your application running in your cluster.

## 1. Kubernetes discovery
- Open the K8s portal
- 

# Kubernetes Multicontainer 
1. Kubernetes multi container app deployment 
- Get the sample code for a multi container application here **TODO LINK**
- Build the container images for frontend and backend services 
- Push the images to your ACR **TODO PUSH to ACR**
- Apply the container images in your Kubernetes cluster using the *.yml files provided 
    - calcbackend-pod.yml
    - calcbackend-svc.yml
    - calcfrontend-pod.yml
    - calcfrontend-svc.yml
- Configure your application to be accessible from the internet and call the page. Use the square calculation.

2. AI **TODO**

**TODO AI**

2. Manual deployment via ReplicationController 
Let's see what happens if one of your pods fails.
- Delete the frontend pod using the commandline and call the website again. 
- You'll recognize that it will no longer work.
Let's configure it for self-healing.
- Apply the replication controller yaml file
    - frontend-rc.yml
- This will take care of starting new instances whenever one of your pods fails. Try to kill the application again by deleting frontend pods and see if your website stays responsive.



# Fully automated VSTS YAML deployment
1. Create a deployment file to decribe the desired state of your application including replicas of your backend service.
    - **TODO Sample?**
    - Modify the deployment file manually so that 
        - the backend service can be found
        - the backend service is available internally only
        - the correct image is being used
    - Apply the deployment file manually.
2. Check the number of backend pods. K8s will take care to keep the number of available pods as specified.
    - Give it a try and kill some pods. They will be recreated.
3. Add a VSTS release definition. Make sure it
    - triggers when the build has finished
    - deploy your latest image created by the build definition with help of the deployment.yaml file. You can use the Azure CLI task to do this.
    - Use $(Build.BuildNumber) to apply the correct image.
    


# Other
- Rollback
- Kubernetes toolchain ​
- Helm (30) with Ingress Controller (30)​
- Monitorng with OMS for Infrastructure (30)​
​
​
​
​
​