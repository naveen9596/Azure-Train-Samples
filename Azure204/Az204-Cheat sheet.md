### **AZ-204 Certification Cheat Sheet: Essential Azure CLI & PowerShell Commands**  

This cheat sheet provides key **Azure CLI** and **Azure PowerShell** commands required for the **AZ-204: Developing Solutions for Microsoft Azure** certification.  

---

## **1. General Azure CLI & PowerShell Commands**  

| **Task**            | **Azure CLI**                    | **Azure PowerShell**                |
|---------------------|--------------------------------|--------------------------------|
| **Login to Azure** | `az login` | `Connect-AzAccount` |
| **List Subscriptions** | `az account list --output table` | `Get-AzSubscription` |
| **Set Default Subscription** | `az account set --subscription <SUBSCRIPTION_ID>` | `Set-AzContext -SubscriptionId <SUBSCRIPTION_ID>` |

---

## **2. Azure Compute (VMs, App Services, Functions, Containers)**  

### **Virtual Machines (VMs)**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create a VM | `az vm create --resource-group MyResourceGroup --name MyVM --image UbuntuLTS --admin-username azureuser --generate-ssh-keys` | `New-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM" -Image "UbuntuLTS"` |
| List VMs | `az vm list --output table` | `Get-AzVM` |
| Start a VM | `az vm start --name MyVM --resource-group MyResourceGroup` | `Start-AzVM -Name "MyVM" -ResourceGroupName "MyResourceGroup"` |
| Stop a VM | `az vm stop --name MyVM --resource-group MyResourceGroup` | `Stop-AzVM -Name "MyVM" -ResourceGroupName "MyResourceGroup"` |

### **Azure App Services (Web Apps, APIs)**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create an App Service Plan | `az appservice plan create --name MyPlan --resource-group MyResourceGroup --sku B1 --is-linux` | `New-AzAppServicePlan -ResourceGroupName "MyResourceGroup" -Name "MyPlan" -Tier "Basic" -WorkerSize "1"` |
| Create a Web App | `az webapp create --name MyWebApp --resource-group MyResourceGroup --plan MyPlan` | `New-AzWebApp -ResourceGroupName "MyResourceGroup" -Name "MyWebApp" -AppServicePlan "MyPlan"` |
| Deploy from GitHub | `az webapp deployment source config --name MyWebApp --resource-group MyResourceGroup --repo-url <GITHUB_URL> --branch main --manual-integration` | `Set-AzWebApp -ResourceGroupName "MyResourceGroup" -Name "MyWebApp" -GitRepositoryUrl "<GITHUB_URL>"` |

### **Azure Functions (Serverless Computing)**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create a Function App | `az functionapp create --name MyFunction --storage-account MyStorage --resource-group MyResourceGroup --consumption-plan-location eastus` | `New-AzFunctionApp -ResourceGroupName "MyResourceGroup" -Name "MyFunction" -StorageAccountName "MyStorage"` |
| List Function Apps | `az functionapp list --output table` | `Get-AzFunctionApp` |

### **Azure Kubernetes Service (AKS)**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create an AKS Cluster | `az aks create --resource-group MyResourceGroup --name MyAKS --node-count 2 --enable-addons monitoring --generate-ssh-keys` | `New-AzAksCluster -ResourceGroupName "MyResourceGroup" -Name "MyAKS" -NodeCount 2` |
| Get AKS Credentials | `az aks get-credentials --resource-group MyResourceGroup --name MyAKS` | `Import-AzAksCredential -ResourceGroupName "MyResourceGroup" -Name "MyAKS"` |
| Deploy to AKS | `kubectl apply -f deployment.yaml` | `kubectl apply -f deployment.yaml` |

---

## **3. Azure Storage (Blob, Table, File, Queue, Cosmos DB)**  

### **Azure Blob Storage**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create a Storage Account | `az storage account create --name mystorage --resource-group MyResourceGroup --sku Standard_LRS` | `New-AzStorageAccount -ResourceGroupName "MyResourceGroup" -Name "mystorage" -SkuName "Standard_LRS"` |
| Create a Blob Container | `az storage container create --name mycontainer --account-name mystorage` | `New-AzStorageContainer -Name "mycontainer" -Context (Get-AzStorageAccount -ResourceGroupName "MyResourceGroup" -Name "mystorage").Context` |
| Upload a Blob | `az storage blob upload --file myfile.txt --container-name mycontainer --account-name mystorage` | `Set-AzStorageBlobContent -File "myfile.txt" -Container "mycontainer" -Context (Get-AzStorageAccount -ResourceGroupName "MyResourceGroup" -Name "mystorage").Context` |

### **Azure Cosmos DB**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create a Cosmos DB Account | `az cosmosdb create --name mycosmosdb --resource-group MyResourceGroup --kind MongoDB` | `New-AzCosmosDBAccount -ResourceGroupName "MyResourceGroup" -Name "mycosmosdb" -Kind MongoDB` |
| Create a Database | `az cosmosdb sql database create --account-name mycosmosdb --name MyDatabase --resource-group MyResourceGroup` | `New-AzCosmosDBSqlDatabase -AccountName "mycosmosdb" -ResourceGroupName "MyResourceGroup" -Name "MyDatabase"` |

---

## **4. Security & Identity (Azure AD, RBAC, Key Vault)**  

### **Azure Active Directory (Azure AD) & Role-Based Access Control (RBAC)**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create a Service Principal | `az ad sp create-for-rbac --name "MyApp"` | `New-AzADServicePrincipal -DisplayName "MyApp"` |
| Assign Role to User | `az role assignment create --assignee <USER_ID> --role Contributor --scope /subscriptions/<SUBSCRIPTION_ID>` | `New-AzRoleAssignment -SignInName "<USER_EMAIL>" -RoleDefinitionName "Contributor"` |

### **Azure Key Vault**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create a Key Vault | `az keyvault create --name MyKeyVault --resource-group MyResourceGroup --location eastus` | `New-AzKeyVault -ResourceGroupName "MyResourceGroup" -VaultName "MyKeyVault" -Location "eastus"` |
| Store a Secret | `az keyvault secret set --vault-name MyKeyVault --name "MySecret" --value "SuperSecretValue"` | `Set-AzKeyVaultSecret -VaultName "MyKeyVault" -Name "MySecret" -SecretValue "SuperSecretValue"` |

---

## **5. Azure DevOps & CI/CD**  
| **Task** | **Azure CLI** | **Azure PowerShell** |
|---------|-------------|----------------|
| Create Azure DevOps Project | `az devops project create --name MyProject` | No direct equivalent |
| Create a Pipeline | `az pipelines create --name MyPipeline --repository <repo-url> --branch main --repository-type github` | No direct equivalent |
| Run a Pipeline | `az pipelines run --name MyPipeline` | No direct equivalent |

---

This cheat sheet covers **core commands** for **AZ-204 certification**. Would you like a PDF version? 🚀
