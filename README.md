![image](https://github.com/user-attachments/assets/2ded10cd-8374-492b-b10f-9e01fe6212aa)

# Observing and Analyzing Network Traffic with Microsoft Azure

## Part 1: Creating Virtual Machines

1. **Access the Azure Portal**:
   - Navigate to [Azure Portal](https://portal.azure.com/).

2. **Create a Resource Group**:
   - Set up a new resource group for managing your resources.
     ![image](https://github.com/user-attachments/assets/e3c302a6-9a77-463e-98e9-b699a658de37)


3. **Set Up Virtual Machines**:
   - **Windows 10 Virtual Machine**:
     ![image](https://github.com/user-attachments/assets/ab9931f1-290d-4049-9e56-f44a1cda2af4)

     - Assign it to the created Resource Group.
       ![image](https://github.com/user-attachments/assets/6e504a61-c725-4a6f-8e19-a7ed02b25a76)

     - Allow Azure to create a new Virtual Network (Vnet) and Subnet.
       ![image](https://github.com/user-attachments/assets/b47e7293-bcbe-45ce-baa4-7c1a3a2cbc30)

   - **Linux (Ubuntu) Virtual Machine**:
     ![image](https://github.com/user-attachments/assets/7a81fcfd-900e-48db-8e1b-3b0a8b1ed0b6)

     - Assign it to the same Resource Group and Virtual Network as the Windows VM.
       ![image](https://github.com/user-attachments/assets/1e178ef7-4921-4281-9a04-9f91feb27c58)

     - Ensure both VMs are within the same Subnet.
     - Use Username/Password authentication.

> **Note**: Keep both VMs for subsequent parts.

---

## Part 2: Observing ICMP Traffic

1. **Set Up Remote Desktop**:
   - For Mac users, install **Microsoft Remote Desktop**.
   - Connect to your Windows 10 VM via Remote Desktop.
     ![image](https://github.com/user-attachments/assets/e4a432fb-cfb6-4e51-a38f-206c2b43c9ad)


2. **Install and Use Wireshark**:
   - Install Wireshark on the Windows 10 VM.
     ![image](https://github.com/user-attachments/assets/87bdb59e-a21a-425e-aff1-4f8e2ab5d189)

   - Start a packet capture session and filter for **ICMP traffic**.
     ![image](https://github.com/user-attachments/assets/4c36d7df-59f6-42d0-ab1c-0418deac551e)
     ![image](https://github.com/user-attachments/assets/594c87aa-a819-4a5e-8160-07a29612de25)



3. **Test Ping Between VMs**:
   - Retrieve the **private IP address** of the Ubuntu VM.
   - Ping the Ubuntu VM from the Windows 10 VM and observe ICMP packets in Wireshark.
     ![image](https://github.com/user-attachments/assets/240936c5-c3de-4dbb-8c79-9397257caaab)

   - Test public website ping (e.g., `www.google.com`) and observe traffic in Wireshark.
     ![image](https://github.com/user-attachments/assets/c2fe1021-a942-477b-8383-0ce793c5e096)


---

## Part 3: Network Security Group Configuration

1. **Manage ICMP Traffic**:
   - From the Windows VM, initiate a continuous ping to the Ubuntu VM.
     ![image](https://github.com/user-attachments/assets/e616881e-c259-4b80-ba3f-3f480b23d2d1)

   - Disable **inbound ICMP traffic** in the Network Security Group for the Ubuntu VM.
     ![image](https://github.com/user-attachments/assets/20863c42-3f6b-4ea7-a634-2ec79e0ebfb5)

   - Observe blocked traffic in Wireshark and the command line.
     ![image](https://github.com/user-attachments/assets/2e38ac3f-a50a-4ee1-b764-7dce82e09e08)

   - Re-enable ICMP traffic and confirm resumed ping activity.
     ![image](https://github.com/user-attachments/assets/451662b7-03da-425f-a909-0e07267b5a61)
     ![image](https://github.com/user-attachments/assets/f4ddda50-8e6e-4c45-b717-c679805fe7c0)
     ![image](https://github.com/user-attachments/assets/9d108afd-1eb3-4959-8169-aaff3c02cf27)




2. **Monitor SSH Traffic**:
   - Start packet capture in Wireshark filtering for **SSH traffic**.
     ![image](https://github.com/user-attachments/assets/6f0b2058-f1f2-4c06-834f-75eb9b8dda88)

   - SSH into the Ubuntu VM from the Windows VM using its private IP.
     ![image](https://github.com/user-attachments/assets/3f7ab0f3-89c5-498a-a051-035234fe6e1f)

   - Observe SSH activity in Wireshark while interacting with the Ubuntu VM.
     ![image](https://github.com/user-attachments/assets/1924a850-cd28-4108-88c9-d2273249a873)
     ![image](https://github.com/user-attachments/assets/91470c7b-d921-45eb-a16e-ed2da8a14dc3)



3. **Analyze DHCP Traffic**:
   - In Wireshark, filter for **DHCP traffic**.
     ![image](https://github.com/user-attachments/assets/96259fc3-6c62-41a5-aa53-b85ec63fd36b)

   - Run `ipconfig /renew` in PowerShell on the Windows VM to request a new IP.    
   - Observe DHCP traffic in Wireshark.
      ![image](https://github.com/user-attachments/assets/0958e9c6-d880-49c6-a478-3a0230c84029)
  

4. **Inspect DNS Traffic**:
   - Filter for **DNS traffic** in Wireshark.
     ![image](https://github.com/user-attachments/assets/730b74ec-18a6-478b-8e3a-1bfe62131a5a)
   - Use `nslookup` in the Windows VM command line to query `disney.com`.
   - Observe DNS activity in Wireshark.
     ![image](https://github.com/user-attachments/assets/215501f4-92fa-4173-b13e-2f4571af73b0)


5. **Explore RDP Traffic**:
   - Filter for **RDP traffic** (`tcp.port == 3389`) in Wireshark.
   - Notice continuous traffic as RDP streams the live connection between machines.
     ![image](https://github.com/user-attachments/assets/481a6b11-e2d4-4df2-815f-569ca7f7db98)


---

## Cleanup

1. Close Remote Desktop connections.
2. Delete the Resource Group(s) created during the lab.
3. Verify Resource Group deletion to ensure no residual resources remain.

---

## Summary

This lab demonstrates:
- Setting up virtual environments in Azure.
- Analyzing network traffic using Wireshark.
- Configuring security settings to control network access effectively.
