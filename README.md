## Lab: Building Your Own Azure Active Directory Domain

In this lab, we'll set up a basic Active Directory environment in Azure. This is a crucial skill for anyone working in IT, especially cybersecurity. We'll be creating a domain controller and a client machine, and we'll focus on the network connectivity aspects.

**1. Setting Up the Domain Controller (DC-1) - The Heart of the Network**

* **Why?** The domain controller is the server that manages user accounts, security policies, and other essential network resources.
* **Create a Resource Group:**
    * Log in to the Azure portal.
    * Click "Resource groups" -> "Create."
    * Name it something like "ADLab-RG."
    * **Explanation:** Resource groups help organize your Azure resources.
    * **Screenshot Hint:** Take a screenshot of the resource group creation page before you click create.
* **Create a Virtual Network and Subnet:**
    * In the same resource group, click "Virtual networks" -> "Create."
    * Name it something like "ADLab-VNet."
    * **Explanation:** The virtual network provides a private network in Azure for your VMs. The subnet divides the network into smaller segments.
    * **Screenshot Hint:** Capture a screenshot of the Virtual Network configuration page.
* **Create the Domain Controller VM (DC-1):**
    * Click "Virtual machines" -> "Create."
    * Name: "DC-1."
    * Image: Windows Server 2022 Datacenter.
    * Size: Choose a basic size (e.g., Standard_B2ms).
    * Username: "labuser."
    * Password: "Cyberlab123!"
    * Attach it to "ADLab-Vnet"
 ![image](https://github.com/user-attachments/assets/e01de368-06c0-45ae-ab65-0b8fc7c648cc)
      ![image](https://github.com/user-attachments/assets/62d7b7b2-030f-4e08-9d5e-ea063d28f8dd)
    * **Explanation:** This VM will be our domain controller.
   
* **Set Static Private IP Address:**
    * Go to the "DC-1" VM's "Networking" settings.
    * Click on the network interface.
    * Go to "IP configurations" and set the private IP address to "Static."
      ![image](https://github.com/user-attachments/assets/dd2471e8-12f0-40cc-8470-531fb5d538c7)
    * **Explanation:** A static IP address ensures that the domain controller's address doesn't change.
   
* **Disable Windows Firewall:**
    * Log in to "DC-1" via RDP.
    * Open "Windows Defender Firewall with Advanced Security."
    * Disable the firewall for all profiles (Domain, Private, Public).
      ![image](https://github.com/user-attachments/assets/fb3e1bc8-a678-480a-8aa0-26da55360aeb)
    * **Explanation:** For this lab, we're disabling the firewall for easier testing. In a real environment, you'd configure firewall rules.
    * **Screenshot Hint:** Take a screenshot of the Windows Firewall with Advanced Security main screen showing that the firewall is off.

**2. Setting Up the Client Machine (Client-1) - Joining the Domain**

* **Why?** The client machine will simulate a typical user's workstation.
* **Create the Client VM (Client-1):**
    * In the same resource group, click "Virtual machines" -> "Create."
    * Name: "Client-1."
    * Image: Windows 10 Pro.
    * Size: Choose a basic size (e.g., Standard_B2ms).
    * Username: "labuser."
    * Password: Whatever you want
    * Attach it to "ADLab-VNet" 
    * **Explanation:** This VM will be our client machine.
 
* **Set DNS Settings:**
    * Go to the "Client-1" VM's "Networking" settings.
    * Click on the network interface.
    * Go to "DNS servers" and set the "Custom" DNS server to the private IP address of "DC-1."
      ![image](https://github.com/user-attachments/assets/ea7c5406-5aa1-40db-9756-5ad9bc4e0a44)
    * **Explanation:** This tells the client machine to use the domain controller for DNS resolution.
    
* **Restart Client-1:**
    * Restart "Client-1" from the Azure portal.
* **Test Connectivity:**
    * Log in to "Client-1" via RDP.
    * Open Command Prompt or PowerShell.
    * Ping "DC-1's" private IP address.
      ![image](https://github.com/user-attachments/assets/cf2f3090-111c-47ed-8946-ac418ab6514d)
    * **Explanation:** This verifies network connectivity between the client and the domain controller.
   
* **Verify DNS Settings:**
    * Open PowerShell and run `ipconfig /all`.
    * Verify that the "DNS Servers" entry shows "DC-1's" private IP address.
      ![image](https://github.com/user-attachments/assets/a6f74396-f845-4b18-b076-62541a4f3f53)
    * **Explanation:** This confirms that the client is using the domain controller for DNS.
    

**3. Finishing Up (and Saving Costs)**

* **Do not delete the VMs.** We'll use them in future labs if you are following along.
* **To save costs:**
    * In the Azure portal, "Stop" or "Deallocate" the VMs when you're not using them.
   
