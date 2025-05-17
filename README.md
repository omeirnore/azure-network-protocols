<p align="center">
  <img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination" width="450"/>
</p>

<h1>Observing Network Traffic and Network Security Group (NSG) Functions Between Azure Virtual Machines</h1>

This project focuses on analyzing network traffic between two Azure virtual machines using Wireshark and PowerShell. It also demonstrates how Network Security Groups (NSGs) can control traffic flow between resources in a virtual network.
<h2>🧰 Prerequisite</h2>

- [Creating Virtual Machines in Azure](https://github.com/omeirnore/VirtualMachine-Creation)
 <h2>🖥️ Environments and Tools Used</h2>

- Microsoft Azure (Virtual Machines, Networking, NSGs)
- Remote Desktop (RDP on Windows 11)
- PowerShell
- Wireshark (Network Protocol Analyzer)
- Network Protocols Observed: SSH, RDP, DNS, HTTP/S, ICMP, DHCP

<h2>🧑‍💻 Operating Systems Used</h2>

- Windows 11 (host system)
- Windows 10 Pro (22H2) [VM]
- Ubuntu Server 22.04 [VM]
<h2>🔌 Step 1: Connect to Windows VM and Install Wireshark</h2>

- Start by logging into the [Azure Portal](https://portal.azure.com/) and navigating to the **Virtual Machines** section.

- Select both the Windows and Linux VMs and click the **Start** button to power them on.  
  *Note: Make a note of the **public IP address** of your Windows VM — you'll need it shortly.*

  <!-- Screenshot: Starting VMs and viewing public IPs -->
  <p><img src="images/step1-start-vms-and-get-ip.png" width="750" alt="Start VMs and check public IPs in Azure" /></p>

- Once the VMs are running, open the **Remote Desktop Connection** tool in Windows.

- In the **Computer** field, enter the public IP address of your Windows VM.  
  Use the friendly name "windows-vm" and check the box for "Reconnect if the connection is dropped."

  <!-- Screenshot: RDP setup screen with IP and friendly name -->
  <p><img src="images/step1-rdp-setup.png" width="750" alt="Remote Desktop Connection setup" /></p>

- Enter the **username and password** you set up for the VM during deployment.

  <!-- Screenshot: Entering RDP credentials -->
  <p><img src="images/step1-enter-credentials.png" width="750" alt="Entering credentials for RDP" /></p>

- Once connected, open **Microsoft Edge** in the Windows VM and navigate to [Wireshark.org](https://www.wireshark.org).

- Download the **Windows x64 Installer**, run the setup, and complete the installation with default options.

<h2>📡 Step 2: Observe ICMP Traffic Using Wireshark and PowerShell</h2>

- Open **Wireshark** inside the Windows VM.

- Select the active **Ethernet interface** and click the **shark fin icon** to begin capturing packets.

  <!-- Screenshot: Start Wireshark capture -->
  <p><img src="images/step2-wireshark-start.png" width="750" alt="Starting capture in Wireshark" /></p>

- In the filter bar, type `icmp` and press **Enter** to isolate ICMP traffic.

  <!-- Screenshot: ICMP filter applied -->
  <p><img src="images/step2-icmp-filter.png" width="750" alt="Wireshark ICMP filter active" /></p>

- Go back to the **Azure Portal**, select the **Linux VM**, and go to the **Networking** tab.  
  Copy its **private IP address**.

  <!-- Screenshot: Linux VM private IP in Azure -->
  <p><img src="images/step2-linux-private-ip.png" width="750" alt="Private IP of Linux VM" /></p>

- In **PowerShell** on the Windows VM, run:
  ```powershell
  ping <Linux-Private-IP>


  <!-- Screenshot: Wireshark download and installation -->
  <p><img src="images/step1-wireshark-install.png" width="750" alt="Installing Wireshark on Windows VM" /></p>

> ✅ **At this point**, you’re connected to your Windows VM and ready to begin capturing and analyzing network traffic using Wireshark.



