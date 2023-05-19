# **Exercise 4: Azure Sentinel**

In this exercise, you will explore about Microsoft Sentinel, Onboarding Azure Subscriptions and Web App – IaaS server to Sentinel. You will run the queries from Microsoft Sentinel logs and will explore the results.

This exercise includes the following tasks:

  - What is Microsoft Sentinel
  - Onboard Azure Subscription to Azure sentinel
  - Onboard the Web App – IaaS server to sentinel
  -  Explore query logs

## **Task 1: What is Microsoft Sentinel?**

Microsoft Sentinel is a scalable, cloud-native solution that provides:
- Security information and event management (SIEM).
- Security orchestration, automation, and response (SOAR).

 Microsoft Sentinel delivers intelligent security analytics and threat intelligence across the enterprise. With Microsoft Sentinel, you get a single solution for attack detection, threat visibility, proactive hunting, and threat response.  To learn more about Microsoft Sentinel refer: `https://learn.microsoft.com/en-us/azure/sentinel/overview`

Microsoft Sentinel is your bird's-eye view across the enterprise alleviating the stress of increasingly sophisticated attacks, increasing volumes of alerts, and long resolution time frames.
1. **Collect data at cloud scale** across all users, devices, applications, and infrastructure, both on-premises and in multiple clouds.
1. **Detect previously undetected threats** and minimize false positives using Microsoft's analytics and unparalleled threat intelligence.
1. **Investigate threats with artificial intelligence**, and hunt for suspicious activities at scale, tapping into years of cyber security work at Microsoft.
1. **Respond to incidents rapidly** with built-in orchestration and automation of common tasks.

    ![](images/core-capabilities.png "core-capabilities")
    
## **Task 2: Onboard Azure Subscription to Azure sentinel**

In this task, you will onboard the Azure subscription to Azure sentinel by configuring the new Log Analytics workspace from sentinel.

1. In the Azure portal, search **Microsoft sentinel (1)** and select **Microsoft sentinel (2)**.

    ![](images/microsoft-sentinel.png "microsoft-sentinel")
 
1. On the Microsoft Sentinel page, click on **Create**.

    ![](images/correct1.png "Create")

1. If there is no Log Analytic workspace pre-created then click on **+ Create a new workspace**, else continue from step 8.

     ![](images/loganalytics.png "log analytics")

1. Now under **add Microsoft Sentinel to a workspace** page, select **log-analytics** workspace Click on **Add**.

      ![](images/log5.png "click on add")
      
1. Once the Microsoft Sentinel is added you will see another notification that says **Successfully added Microsoft Sentinel**, as shown below.

      ![](images/log6.png)

1. This is the default page you will be taken to once your new Azure Sentinel instance is created.

     ![](images/log7.png "news-sentinel")
     
1. Now, click on **Workbooks (1)** from the left pane under threat management, and search  **WAF (2)** and select **Microsoft Web Application Firewall      (WAF) - Azure WAF (3)** from the search results.

    ![](images/log8.png "news-sentinel")

1. Then from the bottom-right corner of the Azure portal, click on **Save (1)** and then click on **OK (2)** to save the workbook.

    ![](images/402.png "news-sentinel")
    
1. Once the **Workbook** is added, you will see a notification that says **Workbook 'Microsoft Web Application Firewall (WAF) - Azure WAF saved successfully**, as shown below.

   ![](images/sentinel4.png "news-sentinel")

1. On the left-hand blade of the Microsoft Sentinel page, under configuration, click on **Settings (1)** and then click on **Workspace settings (2)**.

     ![](images/log10.png "news-sentinel")

1. On the Log Analytics workspace page, under Connect a data source, click on **Azure virtual machines (VMs)**.

   ![](images/correct2.png "news-sentinel")

1. You will see that the virtual machine is not connected to the Log Analytics Connection. Now, click on **JumpVM-<inject key="Deployment ID" />** to connect with Log Analytics Connection

    ![](images/correct3.png "news-sentinel")
      
1. Click on **Connect**.

    ![](images/correct5.png "news-sentinel")
     
1. Once the VM is connected you will see the notification that says **Successfully connected virtual machine**, as shown below.

    ![](images/correct4.png "news-sentinel")

    >**NOTE**: Azure sentinel will take around 30 minutes to load and display the data, meanwhile you can continue with the lab and we will explore the data            collected by log analytics in task 4.    
     
## **Task 3: Onboard the Web App – IIS server to sentinel**

In this task, you will onboard the web app - IIS server to sentinel by configuring the log Analytics agent.

1. In the Azure portal, navigate to your **JumpVM-rg** resource group and select the Route Table **firewallroute**. 
    
    ![](images1/firewallroute.png)
 
1. On the Route table page, select **Routes (1)** under **Settings** and click on **firewallroute (2)**.
 
    ![](images1/routes.png)
   
1. Under **firewallroute** page, update the **Next hope type** from **Virtual appliance** to **Internet (1)** and click on **Save (2)**.

    ![](images1/Nexthopetype.png)
    
3. Navigate back to your **JumpVM-rg** resource group and select **JumpVM-<inject key="Deployment ID" enableCopy="false"/>**. 
 
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
    
1. In the Microsoft Edge browser, open the Azure portal with **portal.azure.com** and sign in with your login credentials. You can check your credentials in the                **Environment details**.

1. Now, In the Azure portal, search **Log Analytics workspace (1)** and select **Log Analytics workspace (2)** from the search results.

     ![](images/analytics1.png)

1. On the log analytics workspace page, select **log-analytics (1)**, and under settings, click on **Agents (2)** after that expand **Log Analytics agent                instructions (3)**, and then click on **Download Windows Agent [64 bit] (4)**. Copy the **Workspace ID (5)** and **Primary key (6)**, then save it to notepad for later use.

     ![](images1/Agents.png)

1. Now, on your web browser, click on three dots **[...] (1)** and go to **Downloads (2)**.

     ![](images/analytics3.png)

1. You will see a file name **MMASetup-AMD64.exe**, here click on **Open file**.

     ![](images/analytics4.png)

1. On the Microsoft Monitoring Agent Setup Wizard, click on **Next**.

     ![](images/analytics5.png)
   
1. Now under Microsoft Software License Terms, click on **I Agree**.

      ![](images/analytics6.png)
 
1. Under the Destination Folder page leave the path to default, and Click on **Next**.

      ![](images/analytics12.png)

1. Now under Agent Setup Options, select the checkbox **Connect the agent to Azure Log Analytics (OMS)**, then click on **Next**.

      ![](images/analytics8.png)

1. Enter the **Workspace ID (1)** and **Workspace key or Primary key (2)** that you noted in step 2, then click on **Next (3)**.

      ![](images/analytics9.png)

1. Under the Ready to Install page, click on **Install**.

      ![](images/analytics10.png)

1. Once the Microsoft Monitoring Agent configuration is completed successfully, click on **Finish**.

      ![](images/analytics11.png)

1. On the **log analytics workspace** page, click on **log-analytics (1)**, then click on **Agents (2)** under settings and you will see **1 Windows computer connected (3)** 
   >**NOTE**: It will take around 5 minutes, for the log analytics agent to connect with a virtual machine, and wait for it to complete before proceeding with the lab.

      ![](images/agents1.png)

1. To explore more on logs, click on **See them in Logs**.

      ![](images/agents2.png)

1. Here you will see the **MMA** query running automatically, and the query result below it.

     ![](images/agents3.png)

## **Task 4: Explore query logs**

In this task, you will run the queries in Microsoft sentinel to check the health status and usage of Network, Logical Disk, Memory, and Processor for the VM.

1. Now, go back to **Microsoft Sentinel |Overview** page by clicking on **Overview (1)** under General on the left-hand side blade, and then click on **Heartbeat          (2)**.
    
    ![](images/microsoft1.png "news-sentinel")
    
    >**NOTE**: Your heartbeat count may vary from the screenshot above. 

1. Now under the **Logs** page, click on **Run**, here you will see the results of the **union Heartbeat** query in query explorer. Here you can see operations around Network, Logical Disk, Memory, and Processor for VM. If you are not able to see the results, then try to adjust the query editor size and you will be able to see the outcome.

    ![](images/microsoft2.png "news-sentinel")
     
1. You can save the query for later use by clicking on **Save (1)** and then selecting **Save as query (2)**.
  
     ![](images/microsoft3.png "news-sentinel")

1. Now under **Save as query** blade, enter **VMProcess (1)** as the Query name, and then click on **Save (2)**.

    ![](images/503.png "news-sentinel")

1. Once the Query is saved you will see the notification thats says **Successfully saved query**, as shown below.

    ![](images/504.png "news-sentinel")

1. Now click on **Queries**, to browse the saved queries in queries explorer.

    ![](images/505.png "news-sentinel")

1. On the **Queries** page, under All Queries, scroll down to **Other (1)** and then click on **Run (2)** under **VMprocess** to run the saved query.

    ![](images/506.png "news-sentinel")

1. Now click on **X** in the top right corner to return to the **Microsoft sentinel** overview page.

    ![](images/microsoft4.png "news-sentinel")
     
1. On the  Microsoft Sentinel **Overview** page, click on **OTHERS (2)**.

    ![](images1/Others.png "news-sentinel")
    
1.  Now under the **Logs** page, remove the existing code and copy paste this query **union usage**, click on **Run (2)**, Here you will see results of the **union usage** query in query explorer. Here you can see operations around Network, Logical Disk, Memory, and Processor for VM. If you are not able to see the results, then try to adjust the query editor size and you will be able to see the outcome.
        
## **Summary**
 
In this exercise you have covered the following:
   - Explored Microsoft Sentinel 
   - Onboarded Azure Subscription to Azure sentinel 
   - Onboarded the Web App – IaaS server to sentinel 
   - Explored query logs
