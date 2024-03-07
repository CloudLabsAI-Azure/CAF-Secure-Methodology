# **Exercise 3: Azure Firewall Premium**

Azure Firewall is a cloud-native and intelligent network firewall security service that provides the best-of-breed threat protection for your cloud workloads running in Azure. It's a fully stateful, firewall as a service with built-in high availability and unrestricted cloud scalability. It provides both east-west and north-south traffic inspection.

Azure Firewall Premium is a next-generation firewall with capabilities that are required for highly sensitive and regulated environments. It includes the following features:

- **TLS Inspection** - decrypts outbound traffic, processes the data, then encrypts the data and sends it to the destination.
- **IDPS** - A network intrusion detection and prevention system (IDPS) allow you to monitor network activities for malicious activity, log information about this activity, report it, and optionally attempt to block it.
- **URL filtering** - extends Azure Firewall’s FQDN filtering capability to consider an entire URL. For example, `www.contoso.com/a/c` instead of `www.contoso.com`.
- **Web categories** - administrators can allow or deny user access to website categories such as gambling websites, social media websites, and others.
For more information, see `https://learn.microsoft.com/en-us/azure/firewall/premium-features`
 

In this exercise, you will explore Azure Firewall premium features and will add diagnostics settings to the firewall. You will also perform test IDPS for HTTP traffic which helps in the detection of attacks. You will also create Routes, and Subnets in the existing Route table and configure the TLS inspection and Application rules in the firewall policy to perform web testing.

## **Task 1: Add firewall diagnostics settings** 

In this task, you will enable diagnostic settings in Azure Firewall to collect firewall logs.

1. In the Azure portal, navigate to your **JumpVM-rg** resource group and select the AzureFirewall resource.

   ![](images/firewall1.png "search gateway")

2. On the firewall page, under **Monitoring**, select **Diagnostic settings**.

   ![](images/firewall2.png "search gateway")

3. Select **Add diagnostic setting** on the **Diagnostic settings**. 

   ![](images/firewall4.png "search gateway")

4. Enter the **Diagnostic setting name** as **fw-diagnostics**.

   ![](images/firewall3.png "search gateway")

5. Under **Logs**, select **Azure Firewall Application Rule**, and **Azure Firewall Network Rule**.

   ![](images/firewall5.png "search gateway")

6. Under **Destination details**, select **Send to Log Analytics workspace** and then click on **Save**.

   ![](images/firewall6.png "search gateway")


## **Task 2: Test IDPS for HTTP traffic**

Azure Firewall Premium provides signature-based IDPS to allow rapid detection of attacks by looking for specific patterns, such as byte sequences in network traffic, or known malicious instruction sequences used by malware.

In this task, you will test IDPS for HTTP traffic

1. On the JumpVM virtual machine, search for **Command Prompt (1)** and open  **Command Prompt (2)** window.

   ![](images/firewall9.png "search gateway")

1. Type the following command at the command prompt:

   - Replace <your web server address> with Firewall IP.

     `curl -A "HaxerMen" <your web server address>`
 
    ![](images/firewall7.png "search gateway")
 
 1. In the custom prompt you will see your Web server response.
 
    ![](images/firewall8.png "search gateway")
 
 1. Navigate to your **JumpVM-rg** resource group and select **AzureFirewall**.
 
     ![](images1/firewall.png)
 
 1. On the **AzureFirewall** page, select **Logs (1)** under the Monitoring tab and click on **Load to editor (2)** under the **Network rule log data** tab.
 
    ![](images1/loadtoeditor1.png)
 
 1. On the query editor workspace, replace the existing query and past the below-mentioned query **(1)** then click on **Run (2)**.
 
     ```bash
     AzureDiagnostics
     | where ResourceType == "AZUREFIREWALLS"
     | where OperationName == "AzureFirewallIDSLog"
     ```
 
    ![](images1/run1.png)
 
    > [! NOTE]
    > It can take some time for the data to begin showing in the logs. Give it at least a couple of minutes to allow for the logs to begin showing the data.
 
1. Under the **Results** tab, expand the most recent result **(1)** and observe the **msg_s (2)** row.
 
   ![](images1/result1.png)
 
1. Now navigate back to firewall policy and under **Settings** select **IDPS**.
 
   ![](images/firewall10.png "search gateway")
 
1. On the **IDPS** page select the **Signature rules (1)** tab and under **Signature ID**, in the open text box type **2032081 (2)**.
 
   ![](images/firewall11.png "search gateway")
 
1. Select **2032081 (1)** signature id and click on **Edit Rules (2)**.
 
   ![](images/firewall12.png "search gateway")
 
1. Under edit rules, change **Signature Mode** to **Alert and Deny** and click on **Save**.  Wait for the deployment to complete before proceeding.
 
   ![](images/firewall13.png "search gateway")

1. Navigate back to WorkerVM, and run the `curl` command again:

    `curl -A "HaxerMen" <your web server address>`

    Since the HTTP request is now blocked by the firewall, you'll see the following output after the connection timeout expires:

    `curl: (56) Recv failure: Connection was reset`
 
     ![](images/firewall14.png "search gateway")

1. Go to the Monitor logs in the Azure portal and find the message for the blocked request.
 
## **Task 3: Web categories testing**
 
In this task, you will create an application rule to allow access to sports websites.

1. In the Azure portal, navigate to your **JumpVM-rg** resource group and select the Route Table **firewallroute**. 
    
    ![](images1/firewallroute.png)
 
1. On the Route table page, select **Routes (1)** under **Settings** and click on **+ Add (2)**.
 
    ![](images1/addroute.png)
 
1. Under **Add Route** page, enter the below information:
  
    - Route Name: Enter **firewallroute (1)**
    - Address prefix destination: Select **IP Address (2)** from the drop-down list
    - Destination IP address/ CIDR ranges: Enter **0.0.0.0/0 (3)**
    - Next hop type: Select **Virtual appliance (4)** from the drop-down list
    - Next hop address: Enter the **private IP Address** of the Firewall **(5)**.
    - Select **Add (6)**
 
     ![](images1/addrouterule.png)
 
 1. Now select **Subnets (1)** and Click on **Associate (2)**.

       - Under Associate subnets, enter the following details:
  
          - Virtual Network: Select **vnet (3)** from the drop-down list.
          - Subnet: Select **jumpvmsubnet (4)** from the drop-down list.
          - Click on **Ok (5)**.
 
           ![](images1/addsubnet.png)
 
1. Navigate to your **JumpVM-rg** resource group and select **JumpVM-<inject key="Deployment ID" enableCopy="false"/>**. 
 
    ![](images1/selectvm.png)

 1. On the Virtual Machine page, go to the **Overview (1)** tab and click on **Connect (2)** then select **Bastion (3)**.
 
    ![](images1/connect.png)
 
1. On the Bastion page, follow the below-mentioned instructions to connect to the Virtual Machine using Bastion:
 
    - **Username**: Enter **demouser (1)**
    - **Authentication Type**: Select **Password (2)** from the drop-down
    - **Password**: Enter **<inject key="JumpVM Admin Password" enableCopy="true"/> (3)**
    - Click on **Connect (4)**
 
    ![](images1/bastionconnect.png)
 
1. Now, you will be redirected to a new tab where the Bastion VM is opened. If you see the pop-up **See text and images copied to the clipboard**, click on **Allow**.
 
    ![](images1/allowpopup.png)
 
1. Within the Bastion VM, search for **Edge (1)** and select **Microsoft Edge (2)**.
 
    ![](images1/selectedge.png)
 
1. Navigate to the below-mentioned URL and you can see the error **can't reach this page**.
 
   ```
   https://www.nfl.com
   ```
   ![](images1/error.png)
 
1. Navigate back to the other tab, where Azure Portal is opened.
 
1. In the Azure portal, go to your **JumpVM-rg** resource group and select **firewallpolicy**.
 
   ![](images/firewall18.png "search gateway")
 
1. Select **TLS inspection (1)** under the **Settings** tab and enter the below details under the **Key vault** tab:
 
    - Parent policy : Choose **Enabled (2)**
    - Managed Identity: Select **(New) fw-cert-id-ZrNC4l8WLg97D  (3)** from the drop-down list
    - Key Vault: Select **(New) fw-cert-kv-ZrNC4l8WLg97D (4)** from the drop-down
    - Certificate: Select **(New) fw-cert-ZrNC4l8WLg97D (5)** from the drop-down
    - Click on **Save (6)**
 
    ![](images1/tlsinspection.png)
 
1. Now, select **Application Rules (1)** from the **Settings** tab under the Firewall Policy page and select **+ Add a rule collection (2)**.
   
   ![](images/firewall17.png "search gateway")
 
1. Under the **Add a rule collection** page, enter the below details to enable the web application in Bastion VM:
 
    - Name: **GeneralWeb (1)**
    - Rule Collection type: **Application (2)**
    - Priority: **103 (3)**
    - Rule collection group: **DefaultApplicationRuleCollectionGroup (4)**
    - Under **Rules (5)** mention the below details:
      - Name: **AllowSports**
      - Source type: Select **IP Address** from the drop-down list
      - Source: Enter *
      - Protocol: Enter **http,https**
      - TLS inspection: Check TLS inspection
      - Destination Type: Select **Web categories**
      - Destination: Enter `Sports`
     
     - Click on **Add (6)**
 
     ![](images/CAF3.png "search gateway")
 
 1.  Once the deployment completes navigating back to the Bastion VM tab and refresh the page where you have browsed for `https://www.nfl.com`. On the Privacy error connection page, click on **Advanced**.
 
     ![](images1/Advanced.png)
 
 1. Click on **Continue to www.nfl.com (unsafe)**.
 
    ![](images1/unsafe.png)
 
 1. Now you can see the NFL web page.
 
    ![](images/firewall22.png "search gateway")
 
 1. Again, navigate to the other tab, where Azure Portal is opened.
 
 1. In the Azure portal, go to your **JumpVM-rg** resource group and select **AzureFirewall**.
 
     ![](images1/firewall.png)
 
 1. On the **AzureFirewall** page, select **Logs (1)** under the Monitoring tab and click on **Run (2)** under the **Application rule log data** tab.
 
     ![](images1/run.png)
 

## **Task 4: Implement and Test URL filtering**
 
1. Navigate back to the tab where you have opened Bastion VM and browse the below-mentioned URL. You can see the error **can't reach this page**.
 
    ```
    www.nytimes.com/section/world
    ```
 
    ![](images1/error1.png)
 
 
1. Now switch back to the other tab, where Azure Portal is opened and to your **JumpVM-rg** resource group then select **firewallpolicy**.
 
    ![](images/firewall18.png "search gateway")
 
1. Select **Application Rules (1)** from the **Settings** tab under Firewall Policy page and select **+ Add a rule collection (2)**.
 
    ![](images/firewall17.png "search gateway")
 
1. Under **Add a rule collection** page, enter the below details to enable the web application in Bastion VM:

    - Name: **Firewall-rulecollection (1)**
    - Rule Collection type: **Application (2)**
    - Priority: **100 (3)**
    - Rule collection group: **DefaultApplicationRuleCollectionGroup (4)**
    - Under **Rules (5)** mention the below details:
      - Name: **URLFiltering**
      - Source type: Select **IP Address** from the drop-down list
      - Source: Enter *
      - Protocol: Enter **http,https**
      - TLS inspection: Check TLS inspection
      - Destination Type: Select **URL**
      - Destination: Enter `www.nytimes.com/section/world`
     
     - Click on **Add (6)**
 
     ![](images/CAF2.png "search gateway")

1. Once the deployment completes navigating back to the Bastion VM tab and refresh the page where you have browsed for `www.nytimes.com/section/world`. On the Privacy error    connnection page, click on **Advanced**.
 
      ![](images1/Advanced1.png)
 
1. Click on **Continue to www.nytimes.com (unsafe)**.
 
    ![](images1/unsafe1.png)
 
1. Now you validate that the HTML response is displayed as expected in the browser.
 
    ![](images/CAF1.png "search gateway")
 
1. Again, navigate to the other tab, where Azure Portal is opened.
 
1. In the Azure portal, go to your **JumpVM-rg** resource group and select **AzureFirewall**.
 
     ![](images1/firewall.png)
 
1. On the **AzureFirewall** page, select **Logs (1)** under the Monitoring tab and click on **Run (2)** under the **Application rule log data** tab.
 
     ![](images1/run.png)
 
 
 ## **Task 5: DDOS protection (Read-Only)**
 
 ### What is DDoS protection?

Distributed denial of service (DDoS) attacks is some of the largest availability and security concerns facing customers that are moving their applations to the cloud. A DDoS attack attempts to exhaust an application's resources, making the application unavailable to legitimate users. DDoS attacks can be targeted at any endpoint that is publicly reachable through the internet.

Azure DDoS Protection, combined with application design best practices, provides enhanced DDoS mitigation features to defend against DDoS attacks. It's automatically tuned to help protect your specific Azure resources in a virtual network. Protection is simple to enable on any new or existing virtual network, and it requires no application or resource changes.

  ![](images/ddos.png)


### Types of attacks Azure DDoS Protection mitigates

- **Volumetric attacks**: These attacks flood the network layer with a substantial amount of seemingly legitimate traffic. They include UDP floods, amplification floods, and other spoofed-packet floods. DDoS Protection mitigates these potential multi-gigabyte attacks by absorbing and scrubbing them, with Azure's global network scale, automatically.
- **Protocol attacks**: These attacks render a target inaccessible, by exploiting a weakness in the layer 3 and layer 4 protocol stack. They include SYN flood attacks, reflection attacks, and other protocol attacks. DDoS Protection mitigates these attacks, differentiating between malicious and legitimate traffic, by interacting with the client, and blocking malicious traffic.
- **Resource (application) layer attacks**: These attacks target web application packets, to disrupt the transmission of data between hosts. They include HTTP protocol violations, SQL injection, cross-site scripting, and other layers 7 attacks. Use a Web Application Firewall, such as the Azure Application Gateway web application firewall, as well as DDoS Protection to provide defence against these attacks. There are also third-party web application firewall offerings available in the Azure Marketplace.

1. In the Azure portal, search **DDoS protection plans (1)** and then select **DDoS protection plans (2)**.
 
   ![](images/ddos1.png)
 
1. Click on create.
 
    ![](images/ddos2.png)
 
1. On the **DDoS protection** page, provide the information as mentioned below,
   - Subscription: **Leave it as default (1)**.
   - Resource Group: **JumpVM-rg (2)**.
   - Name: Enter **DDoSprotection (3)**.
   - Region: **<inject key="Region" />**
   - Click on **Next-Tags**.
 
     ![](images/ddos3.png)
 
1. On the **Tags** tab, leave everything to default and then  click on **Review + create**.
 
     ![](images/ddos4.png)
  
1. If the validation is passed then  click on **Create**.

    >**NOTE**: It may take a couple of minutes for the workspace to be created.

      ![](images/ddos5.png)
 
1. Once the DDoS protection is added you will see a notification that says **Deployment succeeded**, as shown below.

      ![](images/ddos6.png)
 
1. On the DDoS protection page, under setting click on **Protected resources (1)** and then select the **vnet (2)** and click on **Add (3)**.
 
      ![](images/ddos10.png)

1. On the **Add virtual network  to DDoS plan** blade, provide the information as mentioned below,
    - Subscription: **Leave it as default (1)**.
    - Resource Group: **JumpVM-rg (2)**.
    - Virtual network: Select **vnet (3)**.
    - Click on **Add (4)**
   
      ![](images/ddos8.png)
 
1. Once the Protected resources are added you will see a notification that says **Successfully updated the virtual network vnet**, as shown below.
 
      ![](images/ddos9.png)
 
1. Now, In the Azure portal, search **Firewall Manager (1)** and then select **Firewall Manager (2)**.
 
      ![](images/ddos11.png)

1. Under Deployments, click on **Virtual Networks**, and you will see that you are protected.
 
      ![](images/ddos12.png)
    

    > **Congratulations** on completing the lab! Now, it's time to validate it. Here are the steps:
    > - Navigate to the Lab Validation Page, from the upper right corner in the lab guide section.
    > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
    > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
    > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

## **Summary**
 
In this exercise you have covered the following:
  
   - Added firewall diagnostics settings 
   - Tested IDPS for HTTP traffic
   - Performed Web category testing 
   - Implemented and Tested URL filtering
   - Explored on DDoS protection




