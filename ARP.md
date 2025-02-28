- ARP
    
    **ARP (Address Resolution Protocol)** is a network protocol used to map an **IP address** to a device's **MAC address** within a local area network (LAN). It operates at the **data link layer (Layer 2)** and is essential for communication between devices on the same subnet.
    
    ### 1. **Using `arp -a` in Command Prompt (CMD):**
    
    - **Command:** `arp -a`
    - **Purpose:** Displays the ARP cache of the system. The ARP cache is a table that maps IP addresses to MAC addresses for devices on the local network.
    - **Output Details:**
        - **Internet Address:** The IP addresses of devices on the network.
        - **Physical Address:** The corresponding MAC addresses.
        - **Type:** Specifies whether the entry is dynamic or static.
    
    This is useful for verifying network connections and identifying devices on your network.
    
    ### 2. **Using Wireshark with a Filter:**
    
    - **Filter:** `arp`
    - **Purpose:** Filters out ARP packets from the captured network traffic, showing only ARP requests and responses.
    - **Why MAC Addresses Matter:**
        - ARP is used to resolve IP addresses to MAC addresses on a local network.
        - Observing ARP traffic can help identify devices and diagnose issues such as duplicate IPs or missing devices.
    
    ### Practical Uses:
    
    - **Troubleshooting:** If a device isn't reachable, you can verify if its MAC address is in the ARP cache or check for ARP requests in Wireshark.
    - **Security:** Identifying unauthorized devices on the network by their MAC address.
    - **Optimization:** Diagnosing network delays by observing ARP behavior.
    
