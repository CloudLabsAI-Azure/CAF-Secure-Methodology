# Exercise 2- Secure application  

### Overview

Azure Firewall is a managed, cloud-based network security service that protects your Azure Virtual Network resources. It's a fully stateful firewall as a service with built-in high availability and unrestricted cloud scalability. To learn more about Azure Firewall refer: `https://docs.microsoft.com/en-us/azure/firewall`

Azure Application Gateway is a web traffic load balancer that enables you to manage traffic to your web applications. Traditional load balancers operate at the transport layer (OSI layer 4 - TCP and UDP). To learn more about Application gateway refer: `https://docs.microsoft.com/en-us/azure/application-gateway`

Azure Web Application Firewall provides centralized protection of your web applications from common exploits and vulnerabilities. Web applications are increasingly targeted by malicious attacks that exploit commonly known vulnerabilities. SQL injection and cross-site scripting are among the most common attacks. Preventing such attacks in application code is challenging. It can require rigorous maintenance, patching, and monitoring at multiple layers of the application topology. A centralized web application firewall helps make security management much simpler. To learn more about Azure Web Application Firewall refer: `https://docs.microsoft.com/en-us/azure/application-gateway`

In this exercise, you will deploy an Azure Firewall and Application Gateway with WAF V2 then you will publish an application through it. You'll also test the security of the application and perform a sample attack.

This exercise includes the following tasks:

  - Configure WAF to protect your web application
  - Publish your application to the internet with the application gateway
  - Application Gateway WAF Custom Rule to block IP
  - Attack simulation

 ## **Task 1: Configure WAF to protect your web application**
 
 In this task, you will add Virtual Machine as the Backend pool of the Application gateway and also configure the Application Gateway from the firewall policy.
 
 1. From the Azure **Home** page, search for **Application gateways (1)** from the search bar and select **Application gateways (2)**.
 
      ![](images/searchgateway.png "search gateway")
    
 1. Select your **Application Gateway**.

      ![](images/appgateway.png "select gateway")
      
 1. On the Application gateway blade click on the **Backend pools(1)** under setting and then select **AGBackendtarget(2)**.

     ![](/images1/backendpools.png)
     
 1. On the **Edit backend pool** page, follow the below-mentioned instructions:

    - **Target type**: Select **Virtual Machine (1)** from the drop-down.
    - **Target**: Select **JumpVM-<inject key="Deployment ID" enableCopy="false"/>-nic (2)** from drop-down
    - Click on **Save (3)**

    ![](/images1/editbackendpool.png)
    
1. Once the Backend pools are edited, you will see the notification that says **Successfully added rule collection**, as shown below.

     ![](/images/image309.png)

 1. Navigate back to the home page and search for **Application Firewall Policies (1)** from the search bar and select **Web Application Firewall Policies (2)**.

      ![](images1/firewallpolicies.png)
 
 1. Click on **firewallpolicy** under the Web Application Firewall page and click on **Associated application gateways** under the **Settings** tab from the Application Gateway WAF policy page.

     ![](/images1/firewallpolicy.png)
     
 1. On the **Associated Application gateway** page, click on **+ Add association (1)** and select **Application Gateway(2)**

    ![](/images1/addappilcatiogateway.png)
    
 1. Under the **Associate an application gateway** page, follow the below instructions:

    - **Application Gateway (WAF v2 SKU)**: Select **Application Gateway (1)** from the drop down. 
    - **Check** the box next to **Apply the web Application Firewall policy configuration even if it's different from the current configuration (2)**
    - Click on **Add (3)**

    ![](images1/associateappgateway.png)
    
 ## **Task 2: Publish your application to the internet with the application gateway**
 
In this task, you'll publish an application via Application Gateway by configuring the DNAT rules from the firewall policy.

1.  In the Azure **Home** page, from the search bar search for **Application gateways (1)** and then select **Application gateways (2)**.
 
     ![](images/searchgateway.png "search gateway")
 
1. Select your **Application Gateway**.
 
     ![](images/appgateway.png "select gateway")
 
1. Select the **Frontend public IP address** of the application gateway.
 
      ![](images/image301.png "select gateway")

1.  Copy the **Public Ip address** and save it to notepad for later use.

     ![](images/editing12.png )
    
1. On the Azure Portal **Home** page, search **Azure Firewall (1)** and then select **Firewalls (2)**.

   ![firewall](https://github.com/CloudLabsAI-Azure/AIW-Azure-Network-Services/blob/main/media/Azurefirewallnew.png?raw=true)
    
1. Click on the **AzureFirewall**.

   ![firewall](/images1/azurefirewall.png)
   
1. Select **Firewall Public IP** from the Overview tab.

    ![pip](/images1/firewallIP.png)
    
1. Copy the **Public Ip address** and save it to notepad for later use.

    ![ip](/images1/firewallip1.png)  
     
1. Navigate back on Azure Firewall, Select **Firewall Manager (1)** from the **Settings** tab, and click on **Visit Azure Firewall Manager to configure and manage this firewall (2)**

   ![FM](/images1/firewallmanager.png)
    
1. Select **Azure Firewall Policies (1)** under the **Firewall Manager** page and click on Firewall Policy **firewallpolicy (2)**.

   ![policy](/images1/selectfirewallpolicy.png)
   
1. Select **DNAT Rules (1)** from the **Settings** tab under the **Firewall Policy** page and select **+ Add a rule collection (2)**

   ![rule](https://github.com/CloudLabsAI-Azure/AIW-Azure-Network-Services/blob/main/media/dnat1.png?raw=true)
    
1. Under the **Add a rule collection** page, enter the below details:

    - Name: **afw-contoso-prod-firewall-rulecolection (1)**
    - Rule Collection type: **DNAT (2)**
    - Priority: **100 (3)**
    - Rule collection group: **DefaultDnatRuleCollectionGroup (4)**
    - Under **Rules (5)** mention the below details:
      - Name: **afw-dnat-http**
      - Source type: Select **IP Address** from the drop-down list
      - Source: Enter *
      - Protocol: Select **TCP** from the drop-down list
      - Destination Ports: **80**
      - Destination type: Select **IP Address** from the drop-down list
      - Destination: Enter the IP address of the **Firewall** which you copied in step 8.
      - Translated address: Enter the Public IP address of the **Application gateway** which you copied in step 4.
      - Translated port: **80**
     
     - Click on **Add (6)**

       ![rule](/images1/rulecollection.png)
          
1. Now, to test the application copy and paste the Frontend public IP address of **Application Gateway** into a new browser tab that you copied in step 4.

   ![ss](/images/image307.png)
       
  > **Note**: This will confirm that you have published the Contoso web application via Application Gateway.


 ## **Task 3: Application Gateway WAF Custom Rule to block IP** 




 ## **Task 4: Attack simulation** 
     
In this task, you will be testing your application for security and performing sample attacks like XSS. Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser-side script, to a different end-user.

   > **Note**: You can perform this task only after finishing task 2 and task 3.

1. You can perform a sample attack on your application by passing this `?q=<script>` value at the end of the web application URL or IP address.
    
1. Now pass the value `?q=<script>` at the end of your **Application Gateway** IP and try browsing it. You can observe the web application can be still accessible.
  
   > **Note**: Your browsing URL value should look like ```http://20.185.224.102/?q=<script>```
    
   ![ss](/images1/attack.png)
  
1. To make your application more secure, select **ApplicationGateway** from the overview page of the resource group.
     
   ![rp](/images1/rgappgateway.png)
    
1. Under the **Application gateway** page, follow the below details:
     - Select **Web application firewall (1)** under **Settings**    
     - Click on **firewallpolicy** under **Associated web application firewall policy (2)**   
  
     ![config](/images1/webappfirewall.png)
 
1. Under the **firewallpolicy** page, go to the **Overview (1)** tab and click on **Switch to prevention mode (2)**.
 
    ![](/images1/switchtoprevention.png)
    
1. Now, navigate back to the tab where you browsed the IP Address and refresh the page. You can observe the **403 Forbidden error**.
    
    ![server error](/images1/403.png)

## **Task 5: Rate Limiting using Azure Front Door**    
 
     
## **Summary**
 
In this exercise you have covered the following:
  
   - Configured WAF to Protect your web application 
   - Published an application to the internet with the application gateway 
   - Monitored attacks against your web application 
   - Customized WAF rules
   - Performed Attack simulation

Click on the **Next** button present in the bottom-right corner of the lab guide to start with the next exercise of the lab.
