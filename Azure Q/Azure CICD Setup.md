Here’s a **hands-on demo** with a **YAML pipeline script** for an **Azure CI/CD pipeline** that deploys a **Dockerized web application** to **Azure Kubernetes Service (AKS)** using **Azure DevOps Pipelines**.

---

## **Pre-requisites**
1. **Azure DevOps Setup**  
   - Create a repository in **Azure Repos** and push your application code.
   - Enable **Azure Pipelines**.

2. **Azure Resources**
   - **Azure Container Registry (ACR)** for storing Docker images.
   - **Azure Kubernetes Service (AKS)** for deployment.
   - **Terraform/ARM Templates** for infrastructure provisioning (optional).

3. **Azure DevOps Service Connections**
   - Connect to **Azure Subscription**.
   - Create a **Service Connection** to authenticate Azure services.

---

## **Step 1: Define CI Pipeline (azure-pipelines-ci.yml)**  
This pipeline builds the Docker image, runs unit tests, and pushes the image to Azure Container Registry (ACR).

```yaml
trigger:
  branches:
    include:
      - main

pool:
  vmImage: 'ubuntu-latest'

variables:
  acrName: 'myacrname'  # Replace with your ACR name
  imageName: 'myapp'
  tag: '$(Build.BuildId)'

steps:
- task: UseDotNet@2
  inputs:
    packageType: 'sdk'
    version: '6.x'  # Adjust based on your app (.NET, Node.js, etc.)

- script: |
    echo "Building Docker image..."
    docker build -t $(acrName).azurecr.io/$(imageName):$(tag) .
  displayName: 'Build Docker Image'

- script: |
    echo "Running unit tests..."
    dotnet test --logger trx
  displayName: 'Run Unit Tests'

- script: |
    echo "Logging in to ACR..."
    az acr login --name $(acrName)
  displayName: 'Login to Azure Container Registry'

- script: |
    echo "Pushing Docker image to ACR..."
    docker push $(acrName).azurecr.io/$(imageName):$(tag)
  displayName: 'Push Docker Image to ACR'

- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: '$(Build.ArtifactStagingDirectory)'
    artifactName: 'drop'
  displayName: 'Publish Build Artifacts'
```

---

## **Step 2: Define CD Pipeline (azure-pipelines-cd.yml)**  
This pipeline pulls the Docker image from ACR and deploys it to Azure Kubernetes Service (AKS).

```yaml
trigger:
  branches:
    include:
      - main

pool:
  vmImage: 'ubuntu-latest'

variables:
  acrName: 'myacrname'  
  imageName: 'myapp'
  tag: '$(Build.BuildId)'
  aksCluster: 'myakscluster'  # Replace with your AKS cluster name
  resourceGroup: 'myResourceGroup'  # Replace with your Azure resource group

steps:
- task: AzureCLI@2
  inputs:
    azureSubscription: 'myAzureServiceConnection'
    scriptType: 'bash'
    scriptLocation: 'inlineScript'
    inlineScript: |
      echo "Getting AKS credentials..."
      az aks get-credentials --resource-group $(resourceGroup) --name $(aksCluster)

- script: |
    echo "Deploying application to AKS..."
    kubectl apply -f k8s/deployment.yaml
  displayName: 'Deploy to AKS'

- script: |
    echo "Verifying Deployment..."
    kubectl get pods -n default
  displayName: 'Check Deployment Status'
```

---

## **Step 3: Kubernetes Deployment Manifest (k8s/deployment.yaml)**  
Defines how the application will run inside AKS.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
  labels:
    app: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myacrname.azurecr.io/myapp:latest
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: LoadBalancer
  selector:
    app: myapp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

---

## **Step 4: Connect Pipelines in Azure DevOps**
1. **CI Pipeline:**
   - Go to **Azure DevOps** → **Pipelines** → **New Pipeline**.
   - Select **Azure Repos Git**.
   - Choose **Existing YAML file** (`azure-pipelines-ci.yml`).
   - Run the pipeline.

2. **CD Pipeline:**
   - Create another pipeline for `azure-pipelines-cd.yml` and link it to the **CI Pipeline**.

---

## **Step 5: Testing & Monitoring**
- Run `kubectl get services` to get the external IP of the LoadBalancer.
- Access the application in a browser.
- Use **Azure Monitor** and **Application Insights** for real-time monitoring.
- If issues arise, rollback with `kubectl rollout undo deployment myapp-deployment`.

---

## **Deployment Strategy Options**
- **Blue-Green Deployment**: Deploy new version on a separate environment, then switch traffic.
- **Canary Deployment**: Gradually roll out new versions to a subset of users.
- **Rolling Updates**: Update pods incrementally to avoid downtime.

---

### **🚀 Key Benefits**
✅ **Automated** build, test, and deploy  
✅ **Scalable** containerized deployment with AKS  
✅ **Secure** artifact management with ACR  
✅ **Fast rollback** in case of failure  

Would you like a **Terraform script** for provisioning the infrastructure as well? 😊
