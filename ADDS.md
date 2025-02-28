- AD DS
    
    **ADDS** stands for **Active Directory Domain Services**, a core component of Microsoft Active Directory. It provides the tools and framework to manage users, computers, groups, and resources within a network environment. ADDS is commonly used in enterprise environments for centralized management and authentication.
    
    ---
    
    ### **AD DS Configuration on Server**
    
    1. **Install and Add Roles and Features**:
        - Open **Server Manager**.
        - Add the "Active Directory Domain Services" role using the **Add Roles and Features Wizard**.
    2. **Promote Server to a Domain Controller**:
        - After installation, click on the **yellow warning sign** in Server Manager.
        - Choose **Promote this server to a domain controller**.
        - Select **Add a new forest**.
        - Provide a **Root Domain Name** (e.g., `sakshi.in`).
        - Proceed with the default settings, clicking **Next** until installation is complete.
    3. **Set Primary DNS Suffix**:
        - Go to **This PC** > Right-click > **Properties** > **Change Settings**.
        - In the **System Properties** dialog, click **Change**.
        - Click **More** and set the **Primary DNS Suffix** to match the domain (`sakshi.in`).
    4. **Administrator Account**:
        - After setup, the main screen will show the Administrator account as `SAKSHI/administrator`.
    5. **User Management**:
        - To create a single user:
            - Go to **Computer Management** > Local Users and Groups > Users.
            - Add a new user directly.
        - To manage users via AD DS:
            - Open **Active Directory Users and Computers** from Tools in Server Manager.
            - Expand `sakshi.in`.
            - Right-click, select **New > Organizational Unit (OU)**, and name it.
            - Within the OU, create new users as needed.
    6. **Group Policy Management**:
        - Open **Group Policy Management** from Tools.
        - Right-click **Group Policy Objects (GPO)** > **New** > Name the GPO.
        - Edit the GPO:
            - Add users from the OU to the **Security Filtering** section.
    
    ---
    
    ### **Client Configuration**
    
    1. **Join Client to Domain**:
        - Go to **This PC** > Right-click > **Properties** > **Change Settings**.
        - Under **System Properties**, click **Change**.
        - Add the domain name (`sakshi.in`) in the **Domain** field.
    2. **Network Configuration**:
        - Ensure the client and server IP addresses are in the same series (e.g., `192.168.1.x`).
        - Optionally, update DNS records:
            - Open **DNS Manager** on the server.
            - Create a new **Host (AAAA)** record for the client, associating it with its IP address.
    3. **Client Group Policy Updates**:
        - On the server:
            - Go to **Group Policy Management**.
            - Right-click the domain > Create a GPO in this domain and link it here > Name it (e.g., `Test1`).
            - Right-click the GPO > Edit > Configure policies:
                - **User/Computer Configuration** > **Policies** > **Administrative Templates**.
        - On the client:
            - Update Group Policy settings by running the command:
                
                ```
                gpupdate /force
                
                ```
                
    
    ---
    
    ### **Optional Tips**
    
    - **Prevent Accidental Deletion**:
        - When creating an OU, uncheck the "Protect object from accidental deletion" option if deletion might be required later.
    - **Edit Client-Specific Settings**:
        - Use **gpedit.msc** on the client to configure local system policies.
    
    ---
    
    This setup ensures a properly configured AD DS environment with domain-integrated clients, enabling centralized user and policy management.
