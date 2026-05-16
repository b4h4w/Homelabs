## Type 2 hypervisor: Virt-Manager KVM/QEMU

Screenshot of my current homelab which shows how [tracert](https://support.microsoft.com/en-us/topic/how-to-use-tracert-to-troubleshoot-tcp-ip-problems-in-windows-e643d72b-2f4f-cdd6-09a0-fd2989c7ca8e) traversed through firewall interfaces correctly before it goes to the router at 192.168.1.1/24. Also, [nslookup](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/nslookup) confirms my DNS server which resolved to my Windows server IP and Fully Qualified Domain Name (FQDN).

![Current Setuo Screenshot](Screenshots/client-tracert-nslookup-Screenshot.png)

&nbsp;

### Virtual Networks 

- Isolated Network
    - Network: 172.16.0.0/24
    - DHCP range: Disabled
    - Forwarding: Isolated network
- NAT Network
    - Network: 192.168.122.0/24
    - DHCP range: 192.168.122.2-192.168.122.254/24
    - Forwarding: NAT

&nbsp;

### Virtual Machines

- **Firewall**: OPNsense version 26.1  
    - LAN IP: Static 172.16.1.1/24 
    - WAN IP: DHCP leased from Virt-Manager NAT Network
    - Web GUI: http://172.16.1.1
    - DHCP on LAN: Disabled
    - DNS: Unbound as the recursive resolver
        - Listening on LAN interface (172.16.1.1)
        - Domain: opnsense.local
        - Enable DHCP Registration and DHCP Static Mappings
        - Firewall Rules (to be configured - default still)

- **Server**: Windows Server 2022 Data Center version
    - IP: Static 172.16.1.2/24
    - DHCP installed (IP range: 172.16.1.100 - 172.16.1.254/24)
    - DNS installed
    - Default gateway: 172.16.1.1/24
    - Active Directory Domain Services (AD DS)  
        - Domain: winsrv.lab
        - Promoted as Domain Controller

- **Client**: Windows 10
    - IP:  Leased from Windows Server 2022
    - Domain joined

&nbsp;
