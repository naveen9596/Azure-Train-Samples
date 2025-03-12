### **Plan for Providing Azure Credentials for AZ-204 Training**  

To ensure structured **Azure practice** with controlled access, follow this plan:  

---

## **1. Setting Up Azure Credentials**  
### **Option 1: Azure Free Trial (Individual Use)**
- Each trainee can **sign up for an Azure free trial** (valid for **30 days** with $200 credits).  
- Suitable for **self-paced learning** but has limitations on enterprise-level features.  

🔗 **Sign-up Link:** [Azure Free Trial](https://azure.microsoft.com/en-us/free/)  

### **Option 2: Azure Enterprise Subscription (Best for Teams)**
- **Create individual accounts** under your organization’s **Azure subscription**.  
- **Assign role-based access** (RBAC) using **Azure Active Directory (Azure AD)**.  
- **Restrict permissions** to avoid unnecessary costs (Use **Azure Policy & Budgets**).  

✅ **Steps to Create User Credentials:**  
1. **Login to Azure Portal** → Go to **Azure Active Directory**.  
2. Click **Users** → **Add User**.  
3. Choose **"Create User"** → Provide **email and temporary password**.  
4. Assign role **(e.g., Contributor, DevTest Labs User, or Custom Role)**.  
5. Share credentials with the user securely.  

---

## **2. Implementing a 2-Hour Daily Limit for Practice**  
To control **usage time**, use **Azure DevTest Labs** or **Automation Scripts**:  

### **Option 1: DevTest Labs (Recommended)**
- **Create an Azure DevTest Lab** to provide sandboxed environments.  
- **Set auto-shutdown policies** (e.g., **auto-stop after 2 hours**).  
- **Monitor usage & enforce quotas** to prevent overuse.  

🔗 **Learn More:** [Azure DevTest Labs](https://learn.microsoft.com/en-us/azure/devtest-labs/)  

### **Option 2: Automation Script (PowerShell/Azure CLI)**
Schedule an **automated script** to enable/disable user accounts:  
- **Script runs at session start (enable access)**.  
- **Script disables access after 2 hours**.  
- **Alternative:** Use **Azure Logic Apps** for time-based user management.  

---

## **3. Sending Notifications to Manager, NSA Team, and You**  
To track usage and notify relevant stakeholders, configure **Azure Monitor with Alerts**:  

✅ **Steps to Set Up Alerts:**  
1. **Go to Azure Monitor** → **Alerts**.  
2. **Create a new Alert Rule** → Select the required **resource group**.  
3. Define **Conditions**:  
   - **User login/logout events** (via Azure AD Sign-In Logs).  
   - **Resource consumption** (if exceeding predefined limits).  
4. **Set up Actions**:  
   - **Email notification to Manager, NSA Team, and You**.  
   - **Webhook (Optional)** to integrate with Teams/Slack.  

🔗 **Learn More:** [Azure Monitor Alerts](https://learn.microsoft.com/en-us/azure/azure-monitor/alerts/)  

---

## **4. Monitoring & Reporting**  
To **track and review practice sessions**, generate reports using **Azure AD Sign-In Logs**:  
1. **Go to Azure Active Directory** → Select **Sign-In Logs**.  
2. **Filter logs by user and time duration** (2-hour session).  
3. **Export logs weekly** for review by **manager & NSA team**.  

🔗 **Learn More:** [Azure AD Logs](https://learn.microsoft.com/en-us/azure/active-directory/reports-monitoring/concept-sign-ins)  

---

### **Final Execution Plan:**
| Task | Tool/Service | Action |
|-------|-------------|---------|
| **User Account Creation** | Azure AD | Create temporary user accounts with limited access |
| **Session Time Restriction** | DevTest Labs / Automation | Auto-shutdown after 2 hours |
| **Usage Monitoring** | Azure Monitor | Track login, logout, and resource usage |
| **Notification Alerts** | Azure Monitor Alerts | Email notifications to Manager, NSA Team, and You |
| **Usage Reports** | Azure AD Logs | Generate weekly reports for review |

Would you like **detailed scripts** or **step-by-step screenshots** for implementation? 😊
