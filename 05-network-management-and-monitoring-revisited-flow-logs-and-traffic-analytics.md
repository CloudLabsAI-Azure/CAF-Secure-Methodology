# Exercise 6- Network Management and Monitoring Revisited: Flow Logs and Traffic Analytics

Network management and monitoring play a crucial role in maintaining a secure and efficient network infrastructure. In addition to traditional monitoring methods, flow logs and traffic analytics provide valuable insights into network traffic patterns and behavior.

Flow logs capture detailed information about network flows, including source and destination IP addresses, ports, protocols, and packet counts. They offer visibility into network traffic at the packet level, aiding in troubleshooting, detecting anomalies, and understanding network behavior.

Combining flow logs and traffic analytics enables network administrators to gain comprehensive visibility, streamline troubleshooting, and make data-driven decisions for network optimization and security enhancement.

This exercise includes the following tasks:

  - NSG Validation
  - Network Watcher Traffic Analytics to monitor the network
  
## **Task 1: NSG Validation (Optional)**

In this task, you'll access the virtual machine by configuring an inbound port rule in the network security group.

1. Navigate to the Azure portal. Using the search bar, search for **Virtual machines (1)** and **select (2)** from the suggestions.

   ![](images/a18.png "search gateway")
   
1. Select the **JumpVM-<inject key="DeploymentID" enableCopy="false" />** from the list.

   ![](images/a19.png "search gateway")
 
1. From the sidebar, select **Networking** from Settings.

   ![](images/a20.png "search gateway")

1. On the Networking page, Click on **default-allow-rdp (1)** inbound port rule to edit the configuration, select **Deny (2)** from Action and click on **Save (3)**.

   ![](images/a21.png "search gateway")
   
1. On the JumpBox VM, in the search bar, **Search** for **RDP** and **select** the **Remote Desktop Connection** app.
   
   ![](images/a24.png)

1. Paste the **JumpVM DNS Name** in the **Computer** field and click on **Connect**.
   * **JumpVM DNS Name**: **<inject key="JumpVM DNS Name" />**

        ![](images/a25.png)  
 
1. You will see the error **Remote desktop can't be connected to the remote computer** because we are denied the inbound rule for disallowing the RDP and clicking on **OK**.

   ![](images/a27.png)
   
1. Navigate back to the **JumpVM-<inject key="DeploymentID" enableCopy="false" />**, Open Networking tab and click on **default-allow-rdp (1)** inbound port rule to edit the configuration, select **Allow (2)** from Action and click on **Save (3)**.

   ![](images/a28.png)

1. Navigate back on **Remote Desktop Connection**, click on **Connect** and you will see that you are able to connect to the VM.

1. Now, enter the JUMPVM **username**, and **password** provided below and then click on the **OK** button.
    - **Username**: **<inject key="JumpVM Admin Username" />**
    - **Password**: **<inject key="JumpVM Admin Password" />**
   
        ![](images/a30.png)
   
1. Next, click on the **Yes** button to accept the certificate and add in trusted certificates.

   ![](images/a31.png)

## **Task 2: Network Watcher Traffic Analytics to monitor the network**

In this task, you will enable the Traffic Analytics in the NSG flow logs and review the logs.
 
1. Navigate to the Azure portal. Using the search bar, search for **Application gateways (1)** and **select (2)** from the suggestions..
 
     ![](images/searchgateway.png "search gateway")
 
 1. Select your **Application Gateway**.
 
     ![](images/appgateway.png "select gateway")
 
 1. Select the **Frontend public IP address** of the application gateway.
 
     ![](images/image301.png "select gateway")
  
 1. Copy the **Public IP address** and save it to Notepad for later use.

     ![](images/editing12.png )

 1. To test the application copy and paste the Frontend public IP address of **Application Gateway** in a new browser tab and generate some traffic by refreshing the browser.
 
      > **Note**: You will see that your website is running.
 
      ![](/images/image307.png)

1. Navigate to the resource group **JumpVM-rg**, and from the **Overview (1)** tab select the Firewall.

   ![loadbalancer](/images1/firewall.png)
   
1. Select **Firewall Public IP** from the Overview tab.

    ![pip](/images1/firewallIP.png)
    
1. Copy the Public Ip and save it in a text editor.

    ![ip](/images1/firewallip1.png)
      
1. Navigate to the Firewall's public IP address and generate some traffic by refreshing the browser.

   ![pip](/images/a32.png)

1. Navigate back to the Network Watcher and select **Traffic Analytics**, under **Logs** from the options on the left side of the Network Watcher blade.

   ![netwat](https://github.com/CloudLabsAI-Azure/AIW-Azure-Network-Solutions/blob/main/media/traffic.png?raw=true)
      
1. On the **Traffic Analytics** page, set the time interval to the **Last 30 minutes**.

   ![time interval](/images1/timeinterval.png)
   
   > **Note: If you observe the Time interval is greyed out, click on Meanwhile, click here to see just resource data and perform the above step**.

      ![](https://github.com/CloudLabsAI-Azure/AIW-Azure-Network-Solutions/raw/main/media/timeinterval.png)
      
1. Now, you can observe the total number of network traffic flows from **Traffic Visualization**.

    ![traffic visualization](/images1/traffic%20visualisation.png)

    > **Note: The dashboard may take up to 30 minutes to appear when deployed for the first time. This is because Traffic Analytics must first aggregate enough data for it to derive meaningful insights. If it takes more time, you can perform the next task and come back later and check on this**.
           
     
1. Under **Traffic Analytics** Scroll down to **Your Environment** to view the total number of **Deployed Azure regions (1)**, **TA Enabled NSGs (2)**, **Virtual networks (3)**, and **Virtual subnetworks (4)**.

    ![env](/images1/environment1.png)
      
1. To visualize the traffic distribution by geography, click on **View map**. The geo-map shows the traffic distribution to a data center from countries/regions and continents communicating with it.

    ![map](/images1/viewmap.png)
     
1. In the **Traffic Analytics Geo Map View** page, click on the **Green** icon which indicates the Azure region, and observe the resources deployed under the region, to explore more select **More details**.

    ![md](/images1/moredetails.png)
      
1. Under the **More Insights** blade, scroll down and explore traffic distribution for deployments of the East US region.

    ![comm](/images1/moreinsights.png)
     
1. To close the **Traffic Analytics Geo Map View**, click on the cross at the top right corner.

     ![close](https://github.com/CloudLabsAI-Azure/AIW-Azure-Network-Services/blob/main/media/close.png?raw=true)
      
1. Close the **Ports receiving traffic from the Internet** page by clicking the **Cross (X) icon** from the top right corner.
      
1. Under the Traffic Analytics page, scroll down to **Traffic Distribution** to view the analytics of traffic flows across the host, subnet, VNet, and VMSS.

    ![tr](/images1/totaltraffic.png)
     
1. To view the analytics of traffic flows across the host, select **IP (1)**, then select **See all (2)** from **Traffic Distribution**.

    ![td](/images1/ipsee.png)
    
1. You can observe the graph of the **Time trending chart for the top 5 talking IPs** from the **Traffic distribution across the top IPs** page.

    ![see more](/images1/trafficdistri.png)
    
1. Under **Details of top 5 talking IPs**, select VM IP to explore more about traffic distribution.

     ![see more](/images1/top5.png)
     
1. Close the **Traffic distribution across top IPs** by clicking the **cross (X) icon** at the top-left corner of the page.
    
1. In the same way, you can explore more about **Malicious traffic**, and **Blocked traffic** 

1. Now scroll down to **Application ports**, to view analytics for application ports utilized across your environment and select **See all**.

    ![ap](/images1/applicationports.png)
     
1. From the **Most frequent L7 protocols** page, you can explore more about the ports and their ranging.

    ![l7](/images1/l7proto.png)

## **Summary**
 
In this exercise you have covered the following:
  
   - Performed NSG validation.
   - Monitored the network watcher traffic.






















