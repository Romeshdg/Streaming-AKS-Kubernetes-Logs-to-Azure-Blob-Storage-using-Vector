# Streaming-AKS-Kubernetes-Logs-to-Azure-Blob-Storage-using-Vector

# Step1: Login to your Azure portal and Provision an AKS cluster
## Highlights of this project:

🚀Provisioned an AKS cluster using Azure portal or Azure CLI, enabling deployment and management of containerized applications in a highly available and scalable environment.
🚀Deployed an Nginx deployment in a test namespace of the AKS cluster, allowing testing of containerized applications and validating cluster functionality.
🚀Created an Azure blob storage account and container named "akslogs" to store application logs securely and reliably, facilitating log analysis and troubleshooting.
🚀Configured Vector, a high-performance log collector, to access the Azure blob storage container and stream application logs using a configuration file called "vector-config.yaml", ensuring proper storage and analysis of logs.

![01](https://user-images.githubusercontent.com/113555417/224894937-10147d85-0695-406f-8331-5f95b9679f6d.jpg)
![bash](https://user-images.githubusercontent.com/113555417/224894946-ccc2046e-924e-4265-aa42-9ed7121c6aeb.jpg)


# Azure CLI commands
az group create --name MyResourceGroup --location centralindia
az aks create -g MyResourceGroup -n myAKSCluster  --node-count 1 --generate-ssh-keys

![Screenshot 2023-03-11 160601](https://user-images.githubusercontent.com/113555417/224895148-57c8c3d7-6981-4a09-9281-8b14c3131f93.jpg)
![Screenshot 2023-03-11 160601](https://user-images.githubusercontent.com/113555417/224895656-89f5bfbf-1e13-47a3-b84d-e2f634a3a0a4.jpg)


# Step 2: Log in to the cluster and create a deployment
![kubectl](https://user-images.githubusercontent.com/113555417/224895345-e4708dca-cc90-4fc7-86c6-e0eae6596c5f.jpg)


# Step 3: Create Azure blob storage to store the logs
  ##commands
az storage account create \
    --name storageromesh2002 \
    --resource-group MyResourceGroup \
    --location centralindia \
    --sku Standard_ZRS \
    --encryption-services blob

az storage container create \
    --account-name storageromesh2002 \
    --name akslogs \
    
    ![Screenshot 2023-03-11 161717](https://user-images.githubusercontent.com/113555417/224895768-8136ce37-603c-4748-936b-9e0327453da6.jpg)
    
    ![Screenshot 2023-03-11 161953](https://user-images.githubusercontent.com/113555417/224895797-935f7716-de7b-4908-86b6-044fa72adab9.jpg)
    ![Screenshot 2023-03-11 162434](https://user-images.githubusercontent.com/113555417/224895881-766488a5-f7d1-41ac-be15-736b7aaf36ba.jpg)

# Step4: Storage Account Connection String


    ![Screenshot 2023-03-11 163527](https://user-images.githubusercontent.com/113555417/224896011-99fde64a-7add-422c-9205-98fce046b217.jpg)

# Step 5: Prepare vector-config.yaml
    ![Screenshot 2023-03-11 163752](https://user-images.githubusercontent.com/113555417/224896162-44de2f23-c1c1-43a0-9439-05c6d8539d3b.jpg)
# Step 6: Install Vector using Helm
  # command to install the vector
helm repo add vector https://helm.vector.dev
helm repo update
helm upgrade --install vector vector/vector -f vector-config.yaml -n test-ns --version 0.17.1

![vector](https://user-images.githubusercontent.com/113555417/224896377-9d7b8a4f-c257-43a3-b412-243219930c0b.jpg)

# Step 7: The moment of truth!
After a few minutes see the logs streaming to the “akslogs” container in your Azure Blob Storage. 
![akslog](https://user-images.githubusercontent.com/113555417/224896668-9817392c-b7bb-46d6-8832-c83d1996c458.jpg)

![Screenshot 2023-03-11 165548](https://user-images.githubusercontent.com/113555417/224896820-c9353236-a940-44db-8281-e4cc97a43e04.jpg)
![Screenshot 2023-03-11 165559](https://user-images.githubusercontent.com/113555417/224896831-49950a41-a1da-4f94-b1c0-069e9ba3282c.jpg)
![Screenshot 2023-03-11 165617](https://user-images.githubusercontent.com/113555417/224896847-44b1dd88-2fa5-4095-b7c4-1dee854cf573.jpg)

Overall, this project can help organizations effectively manage and leverage their AKS logs for various use cases, such as troubleshooting, performance optimization, security, compliance, and business intelligence.


Thank you!


