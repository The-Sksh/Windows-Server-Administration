- DNS
    
    **DNS (Domain Name System)** is a fundamental system of the internet that translates human-readable domain names (like `www.example.com`) into machine-readable IP addresses (like `192.168.1.1`). This translation allows users to access websites and services using easy-to-remember names instead of complex numerical IP addresses.
    
    ---
    
    ### **SERVER CONFIGURATION**
    
    1. **Install Roles and Features**:
        - Open **Server Manager**.
        - Go to **Manage** > **Add Roles and Features**.
        - Add the **DNS Server** role and complete the installation process.
    
    1. **Create and Configure Forward Lookup Zone**:
        - Open **DNS Manager**.
        - In **DC1**, navigate to **Forward Lookup Zones**.
        - Right-click and choose **New Zone**:
            - Zone Type: **Primary Zone**.
            - Zone Name: `sakshi.in`.
            - Zone File: Create or use the default.
            - Allow both **secure and nonsecure** dynamic updates.
    2. **Add Host Records**:
        - Under the `sakshi.in` zone, add **Host (A)** records for:
            - `AA` with the IP addresses of `Client 1` and `Client 2`.
    3. **Activate the Zone**:
        - Ensure the zone `sakshi.in` is activated and configured properly.
    4. **Configure Server Network Settings**:
        - Change the server’s **DNS settings** to point to its own IP address:
            - Set DNS to `127.0.0.1` (loopback address).
    5. **Verify Zone Resolution**:
        - Open **Command Prompt** on the server.
        - Use the `nslookup` command to test resolution:
            
            ```
            nslookup sakshi.in
            
            ```
            
        - Ensure the IP addresses of both clients are resolved correctly.
    6. **Dynamic Updates**:
        - In **DNS Manager**, right-click the `sakshi.in` zone > **Properties**.
        - Set **Dynamic Updates** to: **Secure and Nonsecure**.
    
    ---
    
    ### **CLIENT CONFIGURATION**
    
    1. **Network Settings**:
        - Set the network adapter to **Bridge Adapter** (if using a virtual environment).
        - Configure IP settings:
            - Obtain the **upper portion** of the IP automatically.
            - Set the **lower section** (DNS Server) to the IP of the DNS Server.
    2. **Verify DNS Resolution**:
        - Open **Command Prompt**.
        - Test DNS resolution for the server using:
            
            ```
            nslookup sakshi.in
            
            ```
            
        - Confirm that the server and client IPs are resolved correctly.
    
    ---
    
    ### **DYNAMIC DNS CONFIGURATION**
    
    **DDNS (Dynamic Domain Name System)** is a service that automatically updates the DNS records of a domain in real time, typically used for devices with dynamically assigned IP addresses (such as home routers, security cameras, or remote servers) that frequently change. DDNS ensures that a domain name always points to the correct IP address, even when the IP address changes.
    
    1. **Server Configuration**:
        - In **DHCP Manager**:
            - Right-click the **Scope** > **Properties**.
            - Navigate to the **DNS** tab.
            - Enable **Always dynamically update DNS records**.
            - Select **Discard A and PTR records when lease is deleted**.
    2. **Client Configuration**:
        - Go to **Network Settings** > **Properties** > **Advanced** > **DNS** tab.
        - Enable **Register this connection’s address in DNS**.
        - Open **Command Prompt** and register the DNS:
            
            ```
            ipconfig /registerdns
            
            ```
            
    
    ---
    
    ### **Testing the Configuration**
    
    - **On the Server**:
        - Check for dynamically updated DNS records in the `sakshi.in` zone.
    - **On Clients**:
        - Confirm that the DNS settings allow proper name resolution.
        - Test dynamic registration with:
            
            ```
            nslookup <hostname>
            
            ```
            
    
    This setup enables a fully functional DNS server with support for dynamic updates, ensuring proper name resolution across the network.
