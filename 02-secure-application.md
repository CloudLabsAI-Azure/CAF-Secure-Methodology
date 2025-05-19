# Exercise 2: Secure application 

### Estimated Duration: 120 minutes

## Overview

Azure Firewall is a managed, cloud-based network security service that protects your Azure Virtual Network resources. It's a fully stateful firewall as a service with built-in high availability and unrestricted cloud scalability. To learn more about Azure Firewall refer: `https://docs.microsoft.com/en-us/azure/firewall`

Azure Application Gateway is a web traffic load balancer that enables you to manage traffic to your web applications. Traditional load balancers operate at the transport layer (OSI layer 4 - TCP and UDP). To learn more about Application gateway refer: `https://docs.microsoft.com/en-us/azure/application-gateway`

Azure Web Application Firewall provides centralized protection of your web applications from common exploits and vulnerabilities. Web applications are increasingly targeted by malicious attacks that exploit commonly known vulnerabilities. SQL injection and cross-site scripting are among the most common attacks. Preventing such attacks in application code is challenging. It can require rigorous maintenance, patching, and monitoring at multiple layers of the application topology. A centralized web application firewall helps make security management much simpler. To learn more about Azure Web Application Firewall refer: `https://docs.microsoft.com/en-us/azure/application-gateway`

In this lab, you will deploy an Azure Firewall and Application Gateway with WAF V2 then you will publish an application through it. You'll also test the security of the application and perform a sample attack.

## Lab Objectives

You will be able to complete the following tasks:

- Task 1: Configure WAF to protect your web application
- Task 2: Accessing your application using the application gateway
- Task 3: Application Gateway WAF Custom Rule to block IP
- Task 4: Attack simulation
- Task 5: Rate Limiting using Azure Front Door

## Task 1: Configure WAF to protect your web application
 
In this task, you will add a Virtual Machine as the Backend pool of the Application gateway and also configure the Application Gateway from the firewall policy.
 
 1. From the Azure **Home** page, search for **Application gateways (1)** from the search bar and select **Application gateways (2)**.
 
      ![](images/searchgateway.png "search gateway")
    
 1. Select your **Application Gateway**.

      ![](images/appgateway.png "select gateway")
      
 1. On the Application gateway blade click on the **Backend pools (1)** under Setting and then select **AGBackendtarget (2)**.

     ![](images1/backendpools.png)
     
 1. On the **Edit backend pool** page, follow the below-mentioned instructions:

    - **Target type**: Select **Virtual Machine (1)** from the drop-down.
    - **Target**: Select **JumpVM-<inject key="Deployment ID" enableCopy="false"/>-nic (2)** from drop-down.
    - Click on **Save (3)**.

      ![](images/editbackendpool-1.png)
    
1. Once the Backend pools are saved, you will see the notification that says **Deployment Succeeded**.

   ![](images/editbackendpool-succeeded.png)

1. Navigate back to the home page and search for **Application Firewall Policies (1)** from the search bar and select **Web Application Firewall Policies (WAF) (2)**.

   ![](images1/firewallpolicies.png)
 
1. Click on **firewallpolicy** under the Web Application Firewall page and click on **Associated application gateways** under the **Settings** tab from the Application Gateway WAF policy page.

   ![](images1/firewallpolicy.png)
     
1. On the **Associated application gateway** page, click on **+ Add association (1)** and select **Application Gateway (2)**

   ![](images1/addappilcatiogateway.png)
    
1. Under the **Associate an application gateway** page, follow the below instructions:

    - **Application Gateway (WAF v2 SKU)**: Select **Application Gateway (1)** from the drop down. 
    - **Check** the box next to **Apply the Web Application Firewall policy configuration even if it's different from the current configuration (2)**.
    - Click on **Add (3)**.

      ![](images1/associateappgateway.png)

1. Once the Application Gateway are saved, you will see the notification that says **Updated the Application Gateway**.

   ![](images1/appgateway-notification.png)


## Task 2: Accessing your application using application gateway
 
In this task, you will access the application by going through the Application Gateway that you just configured.

1.  In the Azure **Home** page, from the search bar search for **Application gateways (1)** and then select **Application gateways (2)**.
 
     ![](images/searchgateway.png "search gateway")
 
1. Select your **Application Gateway**.
 
     ![](images/appgateway.png "select gateway")
 
1. Select the **Frontend public IP address** of the application gateway.
 
      ![](images/image301.png "select gateway")

1.  Copy the **Public IP address** and save it to Notepad for later use.

     ![](images/editing12.png )
          
1. Now, to test the application copy and paste the Frontend public IP address of **Application Gateway** into a new browser tab that you copied in step 4.

   ![ss](images/image307.png)
       

## Task 3: Application Gateway WAF Custom Rule to block IP
 
In this task, you will block access from the Lab VM to the Jump VM by configuring a Firewall Policy custom rule. The rule will deny access to the web application by adding the Lab VM’s Public IP in the deny rule.
 
1. In the Azure portal, search for **Virtual Machines (1)** and select it from the results **(2)**.

   ![](images/a156.png "select gateway")
 
1. On Virtual machines page, select **labvm-<inject key="Deployment ID" enableCopy="false"/>**.

   ![](images/a157.png "select gateway")

1. Copy the **Public IP address** and save it to Notepad for later use.

   ![](images/a158.png "select gateway")

1. In the Azure Portal Search **WAF (1)** and then select **Web Application Firewall policies (WAF) (2)**.
 
   ![](images/image302.png "select gateway")
 
1. On the WAF page, select your **firewallpolicy (1)**, and under Settings, click on **Custom rules (2)** and after that click on **+ Add custom rule (3)**.
 
    ![](images/image303-1.png "select gateway")
 
1. On the **Add custom rule** blade, enter the following details:
 
    - Custom rule name: **WAFcustomrule (1)**
    - Rule type: Select **Match (2)**
    - Priority: Enter **1 (3)**.
    - IP address or range: Enter **Public IP address (4)** of the labvm that is copied above in step 3.
    - Click on **Add (5)**.
 
      ![](images/a159-1.png "select gateway")
 
1. Click on **Save**.
 
   ![](images/a171.png "select gateway")

1. Once the custom rule is created you will see the notification that says **Successfully updated the WAF policy**, as shown below.
 
   ![](images/image306.png "select gateway")

1. To make your application more secure, select **ApplicationGateway** from the overview page of the resource group.
     
   ![rp](images1/rgappgateway.png)
    
1. Under the **Application gateway** page, follow the below details:
     - Select **Web application firewall (1)** under **Settings**.    
     - Click on **firewallpolicy (2)** under **Associated web application firewall policy**.  
  
         ![config](images1/webappfirewall.png)
 
1. Under the **firewallpolicy** page, go to the **Overview (1)** tab and click on **Switch to prevention mode (2)**.

   >**Note**: Wait for the firewallpolicy to get updated before proceeding to next step.
 
    ![](images1/switchtoprevention.png)

1. Navigate back to the browser tab where you accessed the application gateway website and **refresh** the tab; you will no longer be able to see the website.

   ![](images/a160.png "select gateway")

   >**Note**: This may take a few minutes to take effect. 

1. Navigate back to **firewallpolicy** page, go to the **Overview (1)** tab and click on **Switch to detection mode (2)**.

   ![](images/a161.png "select gateway")


> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="09e5a606-3e3a-4e3a-bc6b-93380fcde756" />


## Task 4: Attack simulation
     
In this task, you will be testing your application for security and performing sample attacks like XSS. Cross-site scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser-side script, to a different end-user.

Since we are already blocking the Public IP of the Lab VM from accessing the web application. You will want to perform this test from your own machine’s browser. You can perform a sample attack on your application by passing this `?q=<script>` value at the end of the web application URL or IP address.

1. From your own machine's browser, access the application by putting in the **Application Gateway IP** that you looked up in Task 2.
   
    >**Note**: Your browsing URL value should look like ```http://20.185.224.102```

     ![ss](images/image307.png)

1. Now pass the value `?q=<script>` at the end of your **Application Gateway** IP and try browsing it using browser. You can observe that the web application is accessible.
  
    >**Note**: Your browsing URL value should look like ```http://20.185.224.102/?q=<script>```
    
     ![ss](images1/attack.png)
  
1. To make your application more secure, select **ApplicationGateway** from the overview page of the resource group.
     
    ![rp](images1/rgappgateway.png)
    
1. Under the **Application gateway** page, follow the below details:
     - Select **Web application firewall (1)** under **Settings**.    
     - Click on **firewallpolicy (2)** under **Associated web application firewall policy**.  
  
         ![config](images1/webappfirewall.png)
 
1. Under the **firewallpolicy** page, go to the **Overview (1)** tab and click on **Switch to prevention mode (2)**.

     >**Note**: Wait for the firewallpolicy to get updated before proceeding to next step.

    ![](images1/switchtoprevention.png)
    
1. Now, navigate back to the tab where you browsed the IP Address and refresh the page. You can observe the **403 Forbidden error**.
    
    ![server error](images1/403.png)

     >**Note**: This may take a few minutes to take effect.

## Task 5: Rate Limiting using Azure Front Door
  
In this task, you will set up an Azure Front Door configuration that pools two instances of a web application that runs in different Azure regions. This configuration directs traffic to the nearest site that runs the application. Azure Front Door continuously monitors the web application. You will demonstrate automatic failover to the next available site when the nearest site is unavailable. The network configuration is shown in the following diagram:  
  
![](images/a80.png)
  
### Task 5.1: Create a Front Door for your application

Configure Azure Front Door to direct user traffic based on the lowest latency between the two Web App's origins. You'll also secure your Azure Front Door with a Web Application Firewall (WAF) policy.
  
1. In the Azure portal, search for **Front Doors (1)** and select it from the results **(2)**.
  
    ![](images1/search-front-door.png)
  
1. Select **+ Create** to create a Front Door and CDN profile.
  
    ![](images1/create-front-door.png)

1. On the **Compare offerings** page, select **Custom create**. Then select **Continue to create a Front Door**.
  
    ![](images/a55.png)
  
1. On the **Basics** tab, enter or select the following information, and then select **Next: Secret (5)**.
  
    | **Setting**                 | **Value**                                                     |
    | ----------------------------| ------------------------------------------------------------  |
    | Subscription                | Select your subscription (1).                                     |
    | Resource group              | Select the resource group **JumpVM-rg (2)**                       |
    | Resource group location     | <inject key="Region" />                                |
    | Name                        | Enter **Webapp-Contoso-AFD (3)**                                  |
    | Tier                        | Select **Premium (4)**                                            |
  
    ![](images/a152.png)
  
1. On the **Secrets**, Leave it default as same and click on **Next: Endpoint >**.
  
    ![](images/a56.png)
  
1. In the **Endpoint** tab, select **Add an endpoint (1)** and give your endpoint name as **contoso-frontend (2)**. Select **Add** to add the endpoint.
  
    ![](images/a64.png)
  
1. Next, select **+ Add a route** to configure routing to your Web App origin.
  
    ![](images/a57.png)
  
1. On the **Add a route** page, enter name as **myRoute (1)** and click on **Add a new origin group (2)**.
  
    ![](images/a126.png)
  
1. On the **Add an origin group** pane, enter name as **myOriginGroup (1)** and click on **+ Add an origin (2)**.
  
    ![](images/a127.png)
  
1. To add the First origin, enter **OWASP-Main (1)** as the name, **App services (2)** as the origin type, and select **owasp-mainjump<inject key="DeploymentID" enableCopy="false" />.azurewebsites.net (3)** as the host name then click **Add (4)**.
  
    ![](images/a130.png)

1. To add the Second origin, enter **OWASP-Stage (1)** as the name, **App services (2)** as the origin type, and select **owasp-stage<inject key="DeploymentID" enableCopy="false" />.azurewebsites.net (3)** as the host name then click **Add (4)**.
  
    ![](images/a131.png)
  
1. Click on **Add**.
  
    ![](images/a132.png)
  
1. Again select **Add** to add a route.
  
    ![](images/a133.png)
  
1. Select **+ Add a policy** to apply a Web Application Firewall (WAF) policy to one or more domains in the Azure Front Door profile.
  
    ![](images/a59.png)
  
1. On the **Add security policy** page, enter a Name **mySecurityPolicy (1)**. Then select **Domains (2)** you want to associate the policy with from the dropdown. For WAF Policy, select **Create New** to create a new policy. Enter name of policy is **myWAFPolicy (3)** and click on **Create (4)**. Select **Save (5)** to add the security policy to the endpoint configuration.
  
     ![](images/a60-1.png)
  
1. Select **Review + Create**, review the Summary, and then select **Create** to deploy the Azure Front Door profile. It will take a few minutes for configurations to be propagated to all edge locations.

    >**Note:** Wait for the deployment to complete which might take few minutes before moving on to next task.

    ![](images/a61.png)
   

    ![](images/a65.png)
  
### Task 5.2: View Azure Front Door in action
  
Once you create a Front Door, it takes a few minutes for the configuration to be deployed globally. Once complete, access the frontend host you created.
  
1. On the Front Door resource in the **Overview (1)** blade, locate the endpoint hostname that is created for your endpoint. For example, **contoso-frontend-ghbnd2bafvhmbzfs.z01.azurefd.net**. **Copy (2)** this FQDN.
  
    ![](images/a66.png)
    
1. In a new browser tab, navigate to the Front Door endpoint FQDN. The default App Service page will be displayed.
  
    ![](images/a67.png)
   
    >**Note: The application might take around 5 minutes to reflect, you can continue with the next task come back and refresh the page to view the changes**
   
1. To test instant global failover in action, try the following steps **(Step 3 to Step 8 are optional)**:

1. Switch to the Azure portal, search for and select **App Services**.
  
    ![](images/a46.png)

1. Select one of your web apps, then click **Stop**, then click **Yes** to confirm.

    ![](images/a172.png)

1. Switch back to your browser and select Refresh. You should see the same information page.

    ![](images/a67.png)
    
    >**Note: There may be a delay while the web app stops. If you get an error page in your browser, refresh the page**.
  
1. Switch back to the Azure Portal, locate the other web app, and stop it.
  
    ![](images/a173.png)

1. Switch back to your browser and select Refresh. This time, you should see an error message.

    ![](images/a70.png)

### Task 5.3: Create a Rate Limit Rule
  
1. Navigate to the **App Services** tab. Select both of your web apps, then click **Start**, then click **Yes** to confirm.
  
    ![](images/a174.png)

1. In a new browser tab paste the **endpoint** which you copied in the previous task.

    ![](images/OSwap.png)
  
    ![](images/a67.png)
  
1. Click on **Magnifying glass** on the top right corner of the website to search.
  
    ![](images/a72.png)
  
1. Type in any keyword **(e.g. apple)** and you will see a response from the website. As this site is using JSON, try **refresh** in the browser to do the same search again and now you will not see any response message in the website as you saw previously.
  
    ![](images/a73.png)
  
    ![](images/a74.png)  
  
1. In the Azure portal, search for **myWAFPolicy (1)** and select it from the results **(2)**.
  
    ![](images/a79.png)
  
1. On the **myWAFPolicy** page, under Settings, click on **Custom rules (1)** and after that click on **+ Add custom rule (2)**.
  
    ![](images/a75.png)
  
1. On the **Add custom rule** blade, enter the following details
 
    - Custom rule name: Enter **rateLimitRule (1)**.
    - Rule type: Select **Rate limit (2)**
    - Priority: Enter **1 (3)**
    - Rate limit duration: Select **1 minute (4)**
    - Rate limit threshold (requests): Enter **1 (5)**
  
       ![](images/a176.png)
 
1. Under Conditions, enter the information required to specify a match condition to identify requests where the URL contains the string `contoso` and `azurefd`:
  
    - Match type: Select **String**.
    - Match variable: Select **RequestUri**
    - Match values: Enter **contoso** and **azurefd**
    - Click on **Add**.
      
       ![](images/a177.png)
  
1. Select **Save**.
  
    ![](images/firewallpolicysave3.1.png)

1. Return to the **Overview** page of **myWAFPolicy**, then select **Switch to Prevention mode** to update the policy's operating mode.

    ![](images/preventionmode.png)

    >**Note**: Wait for the firewallpolicy to get updated before proceeding to next step.

1. On the **myWAFPolicy** page, under Settings, click on **Policy settings (1)** and you will notice that your block response status code is set to **403 (2)**. Enter **This is a rate limit test (3)** under the block response body and then click on **Save (4)**.
  
    ![](images/a111.png)    
  
1. Navigate back to the website and try **refresh** in the browser, you will see a response from the website.

    ![](images/a178.png)

    >**Note**: It may take a few minutes for the rate limit test policy to become active. Feel free to move on and come back later to test.

1. After getting the response from the website navigate back to the **firewallpolicy** page, go to the **Overview (1)** tab and click on **Switch to detection mode (2)**.

     ![](images/a161.png "select gateway")

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="cc732f3b-1c39-4339-b1c4-b43b2b31b193" />

## Summary
 
In this lab you have covered the following:
  
- Configured WAF to Protect your web application 
- Accessed your application using the application gateway
- Customized WAF rules
- Performed Attack simulation
- Performed Rate Limiting using Azure Front Door

### You have successfully completed the lab. Click on **Next >>** to proceed with next exercise.
