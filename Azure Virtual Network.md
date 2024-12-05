### Azure Virtual Network (VNet) Tutorial

Azure Virtual Network (VNet) is a foundational service in Microsoft Azure that provides private networking within the cloud. VNets enable you to securely connect Azure resources, extend your on-premises networks, and create isolated environments.

---

### **Key Concepts of Azure VNet**
1. **Subnets**: Divide your VNet into smaller address spaces for resource organization and isolation.
2. **IP Addressing**: Assign public, private, or reserved IPs to resources.
3. **Network Security Groups (NSG)**: Define rules to control inbound and outbound traffic to resources.
4. **VNet Peering**: Connect VNets for communication across regions or subscriptions.
5. **VPN Gateway**: Securely connect on-premises networks to Azure VNets.
6. **Azure Bastion**: Secure access to VMs without exposing them to the internet.
7. **DNS Settings**: Configure name resolution for your VNet.

---

### **Step-by-Step Guide to Create a Virtual Network**
1. **Log in to Azure Portal**  
   Navigate to the [Azure Portal](https://portal.azure.com/).

2. **Create a Virtual Network**
   - In the search bar, type "Virtual Network" and select it.
   - Click on **+ Create**.
   - Fill in the required details:
     - **Subscription**: Choose your subscription.
     - **Resource Group**: Use an existing group or create a new one.
     - **Name**: Name your VNet (e.g., "MyVNet").
     - **Region**: Select the region close to your workload.

3. **Configure Address Space**
   - Specify an IP address range in CIDR notation (e.g., `10.0.0.0/16`).

4. **Add Subnets**
   - Define subnets within the VNet (e.g., `10.0.1.0/24` for a subnet named "WebSubnet").

5. **Set up Security**
   - Attach NSGs to subnets or individual resources to manage traffic.

6. **Review and Create**
   - Review your configurations and click **Create**.

---

### **Common Tasks**
#### **1. VNet Peering**
   - Navigate to your VNet.
   - Go to **Peerings** and click on **+ Add**.
   - Select the VNet to peer with and configure peering options.

#### **2. Connecting a Virtual Machine**
   - When creating a VM, assign it to your VNet and a specific subnet.
   - Use a public or private IP based on your needs.

#### **3. Configuring NSGs**
   - Create an NSG and associate it with a subnet or NIC.
   - Define inbound/outbound rules for allowed traffic.

---

### **Hands-On Lab**
1. **Create a VNet with two subnets**: One for web servers and another for database servers.
2. **Deploy VMs in each subnet** and configure internal communication.
3. **Secure the subnets** using NSGs:
   - Allow HTTP/HTTPS to web subnet.
   - Allow only database connections to the database subnet.
4. **Set up VNet Peering** between two VNets for resource sharing.

---

### **Best Practices**
- Use a **consistent CIDR block strategy** for IP addressing.
- Secure sensitive resources with **NSGs and Azure Bastion**.
- Implement **VNet-to-VNet connections** instead of public internet for inter-resource communication.
- Regularly audit **NSG rules** to ensure they align with security requirements.
- Leverage **Azure Monitor** and **Network Watcher** for performance and troubleshooting.

---

Would you like additional resources, such as a practical scenario or specific details about advanced features?
