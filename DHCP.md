- DHCP
    
    Here’s a refined and complete guide to configuring DHCP on a Windows Server and ensuring the client-side configuration is correctly set up. Additional missing steps and clarifications are included for completeness:
    
    ---
    
    ### **Steps to Configure DHCP on Windows Server**
    
    ### **1. Access the DHCP Management Console**
    
    Open the DHCP management console:
    
    ```
    Press `Win + R`, type `dhcpmgmt.msc`, and press Enter.
    
    ```
    
    ### **2. Install the DHCP Server Role**
    
    - Open **Server Manager**.
    - Navigate to **Manage > Add Roles and Features**.
    - In the wizard:
        - Select **Role-based or feature-based installation**.
        - Choose the server you want to install the DHCP role on.
        - Select **DHCP Server** from the roles list and follow the prompts to complete the installation.
    - After installation, click **Complete DHCP Configuration** in the notification area and proceed with the post-installation tasks.
    
    ### **3. Create a New DHCP Scope**
    
    - In the DHCP management console, expand the server node, right-click on **IPv4**, and select **New Scope**.
    - Follow the wizard and provide the following details:
        - **Scope Name**: A meaningful name for the scope.
        - **IP Address Range**: Define the starting and ending IP range (e.g., `192.168.1.100` to `192.168.1.200`).
        - **Subnet Mask**: Specify the subnet mask (e.g., `255.255.255.0`).
        - **Exclusions (optional)**: Reserve specific IP addresses to exclude them from the range.
        - **Lease Duration**: Set the lease duration for IP addresses (e.g., 8 days).
        - **Gateway (Router)**: Enter the default gateway (e.g., `192.168.1.1`).
        - **DNS Servers**: Specify DNS servers (e.g., `8.8.8.8`, `8.8.4.4`).
        - Complete the wizard and activate the scope.
    
    ### **4. Authorize the DHCP Server**
    
    - If the server is part of an Active Directory Domain Services (AD DS) environment:
        - Right-click the DHCP server name in the DHCP console and select **Authorize**.
    - Wait for the server to be authorized. This step ensures only authorized DHCP servers provide IP addresses on the network.
    
    ### **5. Adjust Firewall Settings**
    
    - Ensure the firewall allows DHCP traffic:
        - Open **Control Panel > Windows Defender Firewall > Advanced Settings**.
        - Verify that inbound rules for **DHCP Server (UDP ports 67 and 68)** are enabled.
    - Alternatively, turn off the firewall for testing purposes:
    
    (Note: Turning off the firewall is not recommended for production environments; instead, configure specific rules.)
        
        ```powershell
        netsh advfirewall set allprofiles state off
        
        ```
        
    
    ### **6. Verify Address Leases**
    
    - In the DHCP console, expand the scope, and click on **Address Leases**.
    - Check that IP addresses are being assigned to clients.
    
    ---
    
    ### **Client-Side Configuration**
    
    ### **1. Set IP Address to Automatic**
    
    - On the client machine, configure the network adapter to obtain an IP address automatically:
        - Open **Control Panel > Network and Sharing Center > Change Adapter Settings**.
        - Right-click the active network adapter and select **Properties**.
        - Double-click **Internet Protocol Version 4 (TCP/IPv4)**.
        - Select **Obtain an IP address automatically** and **Obtain DNS server address automatically**.
        - Click **OK** to save changes.
    
    ### **2. Verify Client Configuration**
    
    - On the client machine, check the assigned IP address:
        
        ```powershell
        ipconfig /all
        
        ```
        
    - Ensure the client has received an IP address, subnet mask, gateway, and DNS server from the DHCP server.
    
    ### **3. Renew the IP Address (if needed)**
    
    - If the client does not receive an IP address automatically, release and renew the IP address:
        
        ```
        ipconfig /release
        ipconfig /renew
        
        ```
        
    
    ---
    
    ### **Verification and Troubleshooting**
    
    ### **1. Monitor DHCP Server Logs**
    
    - On the server, review the DHCP logs for any errors:
        
        ```
        C:\Windows\System32\dhcp
        
        ```
        
    
    ### **2. Test Connectivity**
    
    - Ping the gateway (`192.168.1.1`) and DNS server (`8.8.8.8`) from the client machine to ensure proper configuration.
    
    ### **3. Check DHCP Service Status**
    
    - Ensure the DHCP service is running:
        
        ```powershell
        Get-Service -Name DHCPServer
        
        ```
        
    
    ---
    
    INSHORT : 
    
    to open dhcp command: **dhcpmgmt.msc**
    
    SERVER:
    
    - install add roles and features
    - from right click in 1pv4 create scope and give range
    - give gateway 192.168.1.1
    - dns 8.8.8.8
    - firewall off
    - activate the scope compulsorily
    - authorize 1pv4 if its connected to adds.
    - at last check the address lease
    
    WINDOWS:
    
    - give ip address automatic in network setting
