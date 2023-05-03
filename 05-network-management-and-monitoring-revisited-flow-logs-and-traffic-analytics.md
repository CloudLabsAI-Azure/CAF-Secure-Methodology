# Exercise 5- Network Management and Monitoring Revisited: Flow Logs and Traffic Analytics

1. Navigate to Azure portal.Using the search bar, search for **Virtual machines (1)** and **select (2)** it from the suggestions.

   ![](images/a18.png "search gateway")
   
1. Select the **JumpVM-<inject key="DeploymentID" enableCopy="false" />** from the list.

   ![](images/a19.png "search gateway")
 
1. From the sidebar, select **Networking** from Settings.

   ![](images/a20.png "search gateway")

1. Click on **default-allow-rdp (1)** inbound port rule to edit the configuration, select **Deny (2)** from Action and click on **Save (3)**.

   ![](images/a21.png "search gateway")
   
1. On the JumpBox VM, in the search bar, **Search** for **RDP** and **select** the **Remote Desktop Connection** app.
   
   ![](media/a24.png)

1. Paste the **JumpVM DNS Name** in the **Computer** field and click on **Connect**.
   * **JumpVM DNS Name**: **<inject key="JumpVM DNS Name" />**

   ![](media/a25.png)  
 
1. Now, enter the JUMPVM **username**, and **password** provided below and then click on the **Ok** button.
    - **Username**: **<inject key="JumpVM Admin Username" />**
    - **Password**: **<inject key="JumpVM Admin Password />**
   
   ![](media/a26.png) 

