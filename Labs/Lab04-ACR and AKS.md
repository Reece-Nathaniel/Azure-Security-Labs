# Lab 04: Configuring and Securing Azure Kubernetes Service (AKS)

## **Lab Objective**
In this lab, I configured and secured an Azure Kubernetes Service (AKS) cluster and integrated it with Azure Container Registry (ACR). 
The goal was to deploy and validate a containerized NGINX web application using both external and internal access methods, while ensuring proper authentication between AKS and ACR using managed identities.

---

## Step 1: Creating a Resource Group using PowerShell.
I began by creating a **Resource Group** using Bash in a PowerShell window. 
The resource group was called *AZ500LAB09* and was deployed in the *West Europe* region. 
It contained the resources shown in the image below. I ran commands to ensure the Container Registry was registered to the lab environment.


![Bash window](../IMG_2085.jpeg)

---

## Step 2: Verifying Azure Resources
I used the  az acr list --resource-group AZ500LAB09 to verify that both the AKS cluster (`MyKubernetesCluster`) and Azure Container Registry (`rnwaz500acr2025`) were successfully deployed. 
This confirmed the environment was correctly initialised for subsequent steps.

![Verifying Azure Resources](../IMG_2087.jpeg)

---

## Step 3: Creating a Dockerfile and building an image
Next, I attempted to create a Dockerfile using '*echo FROM nginx > Dockerfile*'
I then attempted to store the ACR name dynamically in a variable and build and push the image to the ACR.
I received an error message stating that I was unable to do this due to the SKU of the subscription I was using.
To overcome this, I ran '*az acr import -n $ACRNAME --source docker.io/library/nginx:latest --image sample/nginx:v1*' to import the existing *nginx image* directly into the **ACR**.

![Creating Dockerfile](../IMG_2089.jpeg)

---

## Step 4: Verifying Repositories Within the Azure Portal
I then closed the **Cloud Shell** window and headed to my AZ500LAB09 **Resource Group** within the **Azure Portal**.
I clicked on my ACR, navigated to *Services* and then clicked on my *Repository* 
From here, I could verify that the new container image '*sample/nginx*' had been pushed successfully.

![Verifying Repository](../IMG_2091.jpeg)

---

## Step 5: Verifying Tag
After verifying the presence of the *sample/nginx* image, I then ensured the v1 tag was present identifying the image version.

![Verifying v1 tag](../IMG_2090.jpeg) 

## Step 6: Creating a Kubernetes Cluster
Through the Azure Portal, I created a **Kubernetes Cluster**.
The purpose of this was to ensure I could host, orchestrate, and manage my containerised application - the *nginx web server*. 
I named the **Kubernetes Cluster** '*MyKubernetesCluster*'. 

![Creation of Kubernetes Cluster](../IMG_2094.jpeg) 

## Step 7: Connecting to the Cluster 
Opening a PowerShell window, I ran the *Bash* command 'az aks get-credentials --resource-group AZ500LAB09 --name MyKubernetesCluster' to connect to the Kubernetes Cluster.
I then ran 'kubectl get nodes' to list the nodes of the cluster. This allowed me to verify the connection and status of the nodes.

![Listing nodes](../IMG_2097.jpeg)

---

## Step 8: Granting Permissions of Management
*Bash* was also used within **PowerShell** to grant the Cluster permissions to access the **ACR** and manage its **Virtual Network**.
The commands in the image below were used to assign the *Contributor* role to the **AKS Cluster** for the **Virtual Network**. 

![Role Assignment](../IMG_2098.jpeg) 

___

## Step 9: Deploy an External Service to AKS
I uploaded the *nginxexternal.yaml* and *nginxinternal.yaml* configuration files to Azure Cloud Shell.
The external **YAML** file was then edited to replace *<ACRUniquename>* with the actual name of my **ACR**.
I then saved my changes and applied it to the cluster using *kubectl apply -f nginxexternal.yaml*. 
This deployed the NGINX application and created the associated Deployment and Service resources.

![External service deployment](../IMG_2099.jpeg) 

---

## Step 10: Verifying External Hosted Service 
The command '* kubectl get service nginxexternal*' was ran to get information about the *nginxexternal* service, including its **private IP address**.
Once I had the **private IP address**, I searched it into another browser window to ensure the setup was working correctly.
This was validated when the 'Welcome to nginx!* page showed. 

![Welcome to nginx!](../IMG_2101.jpeg) 

---

## Step 11: Deploying an Internal Service to AKS
Next, I ran the '* code ./nginxinternal.yaml*' command to edit its content and change the *<ACRUniquename>* to the name of my **ACR**. 
After saving the changes, I ran '* kubectl apply -f nginxinternal.yaml*' to apply the changes to the Cluster.
I then ran '* kubectl get service nginxinternal*' to retrieve information about the internal service, making a note of the **IP address** for later steps.

![Internal service deployed in Bash window](../IMG_2105.jpeg)

---

## Step 12: Verifying Access to AKS Internal Hosted Service
In the same *Bash* window, I ran '* kubectl get pods*' to list the pods within the default namespace on the Cluster.
I then made a note of the pod name and used it in the '* kubectl exec -it <pod_name> -- /bin/bash*' command in order to interact with the pod. 
Finally, I ran '* curl http://<internal_IP>*' replacing '*<internal_IP>*' with the **IP address** noted in *Step 11*.
The command validated that connection to the nginx website was successful. 

![Bash nginx connection](../IMG_2104.jpeg)

--- 

## Step 13: Clean Up Resources 
After successfully completing my lab, I headsd to the **Azure Portal** and deleted the *AZ500LAB09* **Resource Group** to terminate the lab environment and avoid incurring any additional costs.

---

## Summary
In this lab, I successfully deployed a containerized NGINX web application to Azure Kubernetes Service (AKS) and integrated it with Azure Container Registry (ACR). I configured IAM permissions for secure image pulls, tested both external and internal access, and validated network communication between cluster resources.





