# **Exercise 1: Azure Security Center/ Microsoft Defender for Cloud**


### **Overview**


Microsoft Defender for Cloud is a Cloud Security Posture Management (CSPM) and Cloud Workload Protection Platform (CWPP) for all your Azure, on-premises, and multicolored (Amazon AWS and Google GCP) resources. You can find more references about Defender for Cloud here: `https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-cloud-introduction`

An Azure Policy definition, created in Azure Policy, is a rule about specific security conditions that you want to be controlled. Built-in definitions include things like controlling what type of resources can be deployed or enforcing the use of tags on all resources.

In this exercise, you will explore Microsoft Defender for Cloud, configuring Security Policies. Then you will fix the resources by securing the score and improving the Secure Posture. You will also explore on Security center and Security benchmark.

This exercise includes the following tasks:

  - Task 1: Exploring Microsoft Defender for Cloud
  - Task 2: Configure Security Policies
  - Task 3: Secure Score
  - Task 4: Improving your Secure Posture
  - Task 5: Exploring Security center and Security benchmark
  
  
## **Task 1: Exploring Microsoft Defender for Cloud**

In this task, you will explore the features of Microsoft Defender for cloud-like Security posture, Workload Protections, Environment settings. 

1. If you have not signed into the Azure portal already, follow the steps from page 1 of the lab guide to sign in.

2. Search for **Microsoft Defender for Cloud (1)** in the  Azure portal search bar and then click on **Microsoft Defender for Cloud (2)**.
    
    ![](images/defender.png "Microsoft Defender")
    
3. Note that the **Subscriptions** icon on the top menu bar allows you to view and filter **subscriptions**. In this lab, we will use only one subscription, but for your reference, selecting different/additional subscriptions will adjust the interface to reflect the security posture for the specified subscription.

    ![](images/defender-subs.jpg)
    
4. Click on the **What’s new button** – a new tab will open with the latest release notes where you can stay updated on the new features, bug fixes and more.

    ![](images/defender-whats-new.jpg)
    
5. Note the high-level numbers at the top menu, this view allows you to see a summary of your Azure subscriptions, assessed resources, active recommendations, and security alerts.

    ![](images/defender-overview.jpg)

6. On the **Overview** page, look at the **Security posture** tile, you can see your current score along with the number of completed controls and completed         recommendations. Clicking on this tile will redirect you to drill-down view across subscriptions.

    ![](images/editing11.png)
      
      > ⭐ Good to know: <br>
      > The higher the score, the lower the identified risk level.

7. On Microsoft Defender for Cloud page, under cloud security click on **Security posture**. Here you can get an overview of your secure score, unhealthy resources,   and recommendations.
    
   ![](images/securityposture1.png "overview security posture")

8. From the **Microsoft Defender for Cloud** page, select **Workload Protections** from the Cloud Security section.

    ![](images/select-workload-protection.jpg)
    
9. On **Workload Protections (1)**, under Cloud Security, you can see the coverage of your **connected resources (2)** for the currently selected subscription. Your    current resource coverage should be **fully covered 100% (3)** which means **full protection**. Additionally, you can also view the recent **security alerts (4)**,    color-coded by severity.

    ![](images/workload-fully-protected.jpg)
    
10. On the Microsoft Defender for Cloud, Under the Management section, Click on the **Environment settings**. Here you'll be able to see the subscription.

    ![](images/settings.png "environment details")
    
11. Select the **subscription or workspace** that you want to protect.

    ![](images/subsciptionss.png "subscriptions")
 
12. Select **Enable all (1)** to enable all the plans for Defender for Cloud and then click on  **Save (2)**.

    ![](images/plans1.png "enabled all")
        
## **Task 2: Configure Security Policies**

In this task, you will explore the security policy and will assign a built-in initiative policy used by Microsoft Defender for Cloud to the JumpVM-rg resource group.

1. Search for **Policy (1)** in the Azure portal search bar and then click on **Policy (2)**.

    ![](images/policy1.png )
    
1. From the left navigation pane, under the **Authoring** section, click on **Definitions (1)**. This is where you can explore the built-in policy definitions and          initiatives. From the top menu use the filter ribbon, set the Definitions Type as **Initiative (2)**, and select **Security Center (3)** from the Category filter.

    ![](images/policy2.png )
    
1. You can now see built-in initiatives used by Microsoft Defender for Cloud. Here click on **Azure Security Benchmark**.

    ![](images/105.png )
  
1. On the **Azure Security Benchmark** Initiative Definition page click on **Assign**.

    ![](images/106.png )

1. On the **Basics** tab, Click on **Scope[...] (1)** and then select **Subscription (2)** and Resource Group **JumpVM-rg (3)**, then click on **Select (4)**, followed by          clicking on **Next (5)**

    ![](images/editing1.png )

1. Under the **Advanced** tab, leave everything as default and click on **Next**.

    ![](images1/advanced2.png)
    
3. Now under the **Parameters** tab, leave everything to default and then click on **Next**.

    ![](images1/parameters.png "environment details")
    
1. Now under the **Remediation** tab, uncheck the box next to **Create Managed Identity (1)** and then click on **Next (2)**.

    ![](images1/remediation.png "environment details")
    
1. Now on the **Non-compliance messages** tab, select all **Policy definitions (1)**, then click on **Review + create (2)**.

    ![](images1/noncompailance.png )
    
1. Now click on **Create**.

    ![](images1/r%2Bc.png )

1. Once the Policy is assigned you will see another notification that says **Creating initiative assignment succeeded** as shown below.

    ![](images/113.png )
    
1. Navigate back on policy, to see current assignments, click on **Assignments** from the left navigation pane under **Authoring**, and here you can see **Azure Security Benchmark** assigned.

    ![](images/114.png )
    
1. Now under the Policy page, click on **Overview (1)** and then click on **Azure Security Benchmark (2)**.

    ![](images/115.png )
    
1. Under the Azure Security Benchmark Initiative compliance page, click on **Non-compliant resources (1)** and then click on a resource from the list **(2)**.

    ![](images/azure12.png )

1. Now you will be able to see the compliance state of the resource in detail.

    ![](images/azure1.png )
    
    
## **Task 3: Secure Score** 

In this task, you will explore Secure score which helps you understand your current security situation and helps you to understand the security situation by giving recommendations.

1. Search **Microsoft Defender for Cloud (1)** and select **Microsoft Defender for Cloud (2)**.

    ![](images/defender.png "Microsoft Defender")

1. On the Microsoft Defender for Cloud overview page, you can see your **secure score**,      click on **Explore your security posture>**.

    ![](images/posture.png "secure score")

1. Click on **Explore your security posture>**. Here you can get an overview of your **secure score, unhealthy resources, and recommendations**.

    ![](images/securescore2.png "overview security posture")
    
1. On the **Recommendations (1)** page, pay attention to the first part of the page; the **summary view (2)**. It includes the current **Secure Score**, progress on       the **Recommendations status** (both completed security controls and recommendations), and **Resource health** (by severity).

    ![](images/secure3.png)
    
1. From the top menu, click on the **Download CSV report** button – this allows you to get a snapshot of your resources, their health status, and the associated            recommendations. You can use this file for pivoting and reporting.

    ![](images/secure4.png)
    
1. Under **Recommendation**, click on **Manage access and permissions** and select **Guest Configuration extension should be installed on machines** from the drop-down    list. 

    ![](images/secure5.png)
    
1. On the top section, notice the following:

   - Title of the recommendation: **Guest Configuration extension should be installed on machines**
   - Severity indicator: **Medium**
   - Freshness interval: **30 Min** 

    ![](images/secure6.png)
    
1. The next important part is the **Remediation Steps** which contain the remediation logic where you can remediate the selected resources. 
1. Under **Affected resources (1)**, **select a resource** (the single Virtual machine **JumpVM-<inject key="Deployment ID" enableCopy="false"/>(2)** on the Unhealthy resources) and click on **Fix (3)**. This will automatically apply the remediation on the selected resource.

    ![](images/121.png)
    
1. This will open a new window - **Fixing resources**, reviewing the implications for this remediation, and clicking on **Fix 1 resource**.

    ![](images/fix1.png)
    
1. Wait for a notification: ✅ **Remediation successful** - Successfully remediated the issues on the selected resources.
   > **Note**: It can take several minutes after remediation completes to see the resources in the 'healthy resources' tab. You can move to the next task and come back                   later to check on this.
    
    ![](images/secure9.png)

## **Task 4: Improving your Secure Posture** 

In this task, you will explore and fix the security recommendations suggested by Microsoft Defender for cloud.

1. Search **Microsoft Defender for Cloud (1)** and Select **Microsoft Defender for Cloud (2)**.

    ![](images/defender.png "Microsoft Defender")
    
1. Click on **Recommendations (1)** from the left side pane. Expand **Remediate vulnerabilities (2)** security control (which contains all recommendations related to      security vulnerabilities). Make sure you have **Machines should have a vulnerability assessment solution (3)** recommendation listed here.

   > Note: If you don't see the above recommendation that means it is not loaded yet and it could take up to 24 hours for all the recommendations to show up. It is possible that during lab time this may not show up – which is the case sometimes. You can note down this step number then continue to the next exercise and verify this later.

    ![](images/posture1.png)

1. Click on **Machines should have a vulnerability assessment solution** recommendation and open it.
1. Click to expand **Remediation steps (1)** – then click on the **Quick fix logic (2)** option to expose an automatic remediation script content (ARM template). Once    done, **Close (3)** this window. 

    ![](images/posture2.png)

1. From the **Affected resources (1)** tab, select  **JumpVM-<inject key="Deployment ID" enableCopy="false"/> (2)** virtual machines.  Click on **Fix (3)**.

   > Note: If you don't see the virtual machine or the virtual machine is in the unloaded     stage, please wait for 5-10 minutes and refresh the page.

    ![](images/123.png)

1. On the **Choose a vulnerability assessment solution**, select **Deploy integrated vulnerability scanner powered by Qualys (included in Microsoft Defender for            servers) **. Click on  **Proceed**.

    ![](images/posture4.png)

1. A window of **Fixing resources** will open, on this page review the list of VMs and click on **Fix 1 resources**.

    ![](images/124.png)

1. Remediation is now in process. Microsoft Defender for Cloud will deploy the Qualys VM extension on the selected VMs, so you can track the status using the notification area or by using the Azure activity log. **Wait for 5-10 minutes for the process to complete**.

1. Ensure the VM extension is deployed on the relevant machines:
    - Search for **Virtual Machines** in the search box located at the top of the **Azure Portal** page and click on it.
    - Select **JumpVM-<inject key="Deployment ID" enableCopy="false"/>**. next, click on **Extensions + applications** under the **Settings** section.
    - Ensure that **WindowsAgent.AzureSecurityCenter** extension is installed, and the status is **Provisioning succeeded**.
   
    ![](images/last4.png)

## **Task 5: Exploring Security Center and Security benchmark**

Azure Security Center by Microsoft is a solution that provides unified security management across hybrid cloud workloads. It offers threat protection for data centers within both cloud workloads and on-premises. In this task, you will explore Security Center and Security benchmark.

### **Task 5.1: Explore Security Center**

1. In the Azure portal, Search **Azure Security Center (1)** and then click **Azure Security Center (2)**. 

    ![](images/securitycentre.png "security centre")
     
1. On Getting started blade, click **Install agents (1)** and then click **Install agents (2)**.

    ![](images/agent.png "security agent")

1. Back on the Getting started blade, click **Upgrade**, and then click **Open security center**.

    ![](images/center1.png "Open security center")

1. On the Microsoft Defender for Cloud blade, under the **General** section, select the **Inventory** button.

    ![](images/defender5.png)

1. Hover over the **Summaries strip** at the top of the page.

    ![](images/defender6.png)

   > **Note**: In your environment, these numbers may not be the same, since it varies in time.

1.  Notice the **total number of resources**, The total number of resources are the ones that are connected to the Microsoft Defender for Cloud and NOT the total           number of resources that you have in your subscriptions.

1. Notice the number of **unhealthy resources**, The unhealthy resources are the resources with actionable recommendations based on the selected filter.

1. Notice the **unmonitored resources**, The unmonitored resources indicate if there are resources with the Log Analytics agent deployed but with health issues. Since we      enabled the auto-provisioning in the previous module, all existing VMs are covered and connected, which means they are monitored.

1. Use the **Filter by name (1)** box to search for **Virtual machine**. You should now see a filtered view containing your desired resource: **JumpVM-<inject key="Deployment ID" enableCopy="false"/>**. Hover on the      red bar in the **recommendations** column to see a tooltip with the **active recommendations (2)**. You should expect to see **Active-xx of xx Recommendations**      these are the active recommendations you must attend.

    ![](images/editing6.png)

1. Open the resource health pane by selecting the resource. Click on **JumpVM-<inject key="Deployment ID" enableCopy="false"/> (1)**. Alternatively, you can also right-click on any resource and select **view           resource**. You may not see **view resource** directly due to different screen resolutions, then you have to click on **ellipse(...) (2)** and then select **view               resource (3)**.

    ![](images/editing7.png)

1. On the resource health pane for **JumpVM-<inject key="Deployment ID" enableCopy="false"/>**, review the virtual machine information alongside the recommendation list.

    ![](images/fix4.png)

    > **Note**: It could take up to 24 hours for all the recommendations to show up. And it is possible that during lab time this may not show up – which is the         case sometimes. If you don't see the data in the **recommendations**. You can continue to the next exercise and verify this later.

1. Go back to the Inventory page in the filter menu, select the **Resource Groups (1)** filter and then provide the value **JumpVM-rg (2)** (Unselect remaining),          and click on **Ok (3)**. Using this filter, you can see all resources related to the predefined Kubernetes resources which are monitored with active                    recommendations.

      ![](images/last1.png)

    > **Note:** The list can be filtered and sorted.
    
1. On the **Inventory** page, Select the virtual machine **JumpVM-<inject key="Deployment ID" enableCopy="false"/>** and then from the top menu, click on **Assign tags**

    ![](images/editing8.png)

1. On the **Assign tags** blade, Assign **Environment** as the name and **Production** as the value, and click on **Save**.

    ![](images/fix7.png)

1. Wait for a notification: ✅ **Successfully assigned the tag**.

    ![](images/defender13.png)
    
1. Select the virtual machine **JumpVM-<inject key="Deployment ID" enableCopy="false"/>** From the top menu bar, click on **Download CSV report (3)**. You will get a      snapshot to work on it offline already filtered. You can also right-click on any of the    resources and upgrade to Microsoft Defender for Cloud plan (when            applicable).

    ![](images/editing9.png)

1. Wait for a notification: ✅ **Your CSV report is ready**.

    ![](images/defender15.png)

1. Select the virtual machine **JumpVM-<inject key="Deployment ID" enableCopy="false"/>** and then from the top menu, click on **Open query**.

    ![](images/editing10.png)
    
1. On the **Azure Resource Graph Explorer** blade, click on **Run Query (1)**. This query is editable based on the requirement.

    ![](images/defender17.png)

1. Save the query for later use by clicking on **Save as** from the top menu. You can use it to create periodic reports. 
   
     ![](images/last2.png)
   
1. Enter name the report as **asc-filtered-query** and click on **save**.
 
      ![](images/defender18.png)

### **Task 5.2: Explore Security benchmark**

1. Search for **Policy (1)** in the Azure portal search bar and then click on **Policy (2)**.

    ![](images/policy1.png)
    
1. Select **Definitions (1)** from the left navigation pane.

1. From the top menu, select **+ Initiative definition (2)** to add a new initiative.

    ![](images/benchmark1.png)
 
1. On the New Initiative definition page, select the following:
    - Initiative location: Select your Subscription.
    - Name: **Contoso Security Benchmark**.
    - Description: **Baseline for security policies to appear alongside the built-in recommendations**.
    - Category: Select **Create new** and type: **Contoso**.
    - Version: **1**.
    - Click **Next**.

    ![](images/benchmark2.png)

1. On the Policies tab, select **Add policy definition(s) (1)**.
1. The Add policy definition(s) pane opens, search **Storage accounts should restrict network access (2)** and select the **Storage accounts should restrict network        access (3)**, and click on **Add (4)**. Select **Review + Create (5)**.

    ![](images/benchmark3.png)

1. Click on **Create**.

    ![](images/benchmark4.png)

1.  Wait for a notification: ✅ **Successfully saved initiative definition**.

    ![](images/benchmark5.png)

### **Task 5.3: Add a custom initiative to your subscription**

1. Search for **Microsoft Defender for Cloud (1)** in the Azure portal search bar and then click on **Microsoft Defender for Cloud (2)**.
    
    ![](images/defender.png "Microsoft Defender")

1. On the Microsoft Defender for Cloud, Under Management Click on the **Environment settings**.

    ![](images/settings.png "environment details")
    
1. Select the **subscription or workspace** that you want to protect.

    ![](images/subsciptionss.png "subscriptions")
        
1. Under policy setting, Click on **Security Policy**.

    ![](images/security1.png)

1. On the Security policy page, under **Your custom initiatives**, click **Add a custom initiative**.

    ![](images/security2.png)

1. Your newly created initiative is listed: **Contoso Security Benchmark**. Select **Add**.

    ![](images/security3.png)

1. On the **Assign Initiative** page leave everything as default and select **Review + Create**.

    ![](images/security4.png)
    
1. Now click on **Create**.

    ![](images/security5.png)

1. Your custom initiative is now assigned.

    ![](images/security6.png)


## Summary
 
In this exercise you have covered the following:
  
   - Configured Microsoft Defender for Cloud 
   - Configured the Security Policies
   - Explored on Secure score
   - Improved the security posture
   - Explored on Security Center and Security benchmark

 Click on the **Next** button present in the bottom-right corner of the lab guide to start with the next exercise of the lab.
