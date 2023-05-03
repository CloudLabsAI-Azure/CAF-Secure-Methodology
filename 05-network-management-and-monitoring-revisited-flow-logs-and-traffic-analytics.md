# Exercise 5- Network Management and Monitoring Revisited: Flow Logs and Traffic Analytics

## Task 1: NSG Validation - New

1. Navigate to Azure portal. Using the search bar, search for **Virtual machines (1)** and **select (2)** it from the suggestions.

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
 
1. you will see the error **Remote destop can't connected to the remote computer** because we are deny the inbound rule for diallow the RDP and click on **OK**.

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

## Task 2: Network Watcher Traffic Analytics to monitor the network - New




























