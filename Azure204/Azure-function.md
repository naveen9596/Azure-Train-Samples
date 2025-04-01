Here’s a simple **Azure Function template** along with a **sample Python code** for a demo function that responds to HTTP requests.

---

## **Azure Function Template for Python**
Azure Functions in Python typically use the **Azure Functions Core Tools** to create and deploy functions. Below is the basic structure:

### **Folder Structure**
```
my-azure-function/
│── function_app/
│   ├── __init__.py
│   ├── function.json
│── host.json
│── requirements.txt
│── local.settings.json
```

### **Sample Python Code for an HTTP-triggered Azure Function**
This function takes a name as input from the query parameters or request body and returns a greeting.

#### **1. Create an Azure Function Locally**
To create a function, use Azure Functions Core Tools:
```sh
func init my-azure-function --python
cd my-azure-function
func new --name HttpTriggerFunction --template "HTTP trigger" --authlevel "anonymous"
```

#### **2. Sample Python Function (`__init__.py`)**
```python
import azure.functions as func
import logging

def main(req: func.HttpRequest) -> func.HttpResponse:
    logging.info("Python HTTP trigger function processed a request.")

    name = req.params.get("name")
    if not name:
        try:
            req_body = req.get_json()
            name = req_body.get("name")
        except ValueError:
            pass

    if name:
        return func.HttpResponse(f"Hello, {name}! Welcome to Azure Functions.", status_code=200)
    else:
        return func.HttpResponse(
            "Please pass a name in the query string or in the request body.",
            status_code=400
        )
```

#### **3. Function Configuration (`function.json`)**
```json
{
    "bindings": [
        {
            "authLevel": "anonymous",
            "type": "httpTrigger",
            "direction": "in",
            "name": "req",
            "methods": ["get", "post"]
        },
        {
            "type": "http",
            "direction": "out",
            "name": "$return"
        }
    ]
}
```

#### **4. Run Locally**
Start the function locally:
```sh
func start
```
Access it via:  
`http://localhost:7071/api/HttpTriggerFunction?name=YourName`

#### **5. Deploy to Azure**
```sh
# Login to Azure
az login 

# Create a function app (Replace <your-function-app-name> with a unique name)
az functionapp create --resource-group <your-resource-group> --consumption-plan-location <your-region> --runtime python --functions-version 4 --name <your-function-app-name> --storage-account <your-storage-account>

# Deploy your function
func azure functionapp publish <your-function-app-name>
```

---

### **Key Takeaways**
✅ **Uses HTTP Trigger** for handling web requests  
✅ **Serverless Execution** with auto-scaling  
✅ **Can be deployed to Azure easily**  
✅ **Supports JSON input processing**  

Would you like a **demo using a different trigger** (e.g., Timer, Blob Storage, Queue)? 😊
