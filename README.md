<p align="center">
  <img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination" width="450"/>
</p>

<h1 align="center">Observing Network Traffic and Network Security Group (NSG) Functions Between Azure Virtual Machines</h1>

This project focuses on analyzing network traffic between two Azure virtual machines using Wireshark and PowerShell. It also demonstrates how Network Security Groups (NSGs) can control traffic flow between resources in a virtual network.

---

<h2>🧰 Prerequisite</h2>

- [Creating Virtual Machines in Azure](https://github.com/omeirnore/VirtualMachine-Creation)

---

<h2>🖥️ Environments and Tools Used</h2>

- Microsoft Azure (Virtual Machines, Networking, NSGs)
- Remote Desktop (RDP on Windows 11)
- PowerShell
- Wireshark (Network Protocol Analyzer)
- Protocols Observed: SSH, RDP, DNS, HTTP/S, ICMP, DHCP

---

<h2>🧑‍💻 Operating Systems Used</h2>

- Windows 11 (host system)
- Windows 10 Pro (22H2) [VM]
- Ubuntu Server 22.04 [VM]

---

<h2>🔌 Step 1: Connect to Windows VM and Install Wireshark</h2>

- Log in to the [Azure Portal](https://portal.azure.com/) and navigate to the **Virtual Machines** section.

- Start both the Windows and Linux VMs.  
  📌 *Note the public IP address of the Windows VM — you'll need it to connect via RDP.*

<p align="center">
  <img src="images/an-1.jpg" width="750" alt="Starting VMs and noting public IPs in Azure" />
</p>

- Open the **Remote Desktop Connection** tool on your Windows 11 host system.

- In the **Computer** field, enter the public IP address of your Windows VM and click **Connect**.

<p align="center">
  <img src="images/an-2.jpg" width="750" alt="Remote Desktop setup screen" />
</p>

- Enter the **username and password** configured during VM setup.

<p align="center">
  <img src="images/an-3.jpg" width="750" alt="RDP login credentials" />
</p>

- Once connected, you'll have full access to your Windows VM:

<p align="center">
  <img src="images/an-4.jpg" width="750" alt="Windows VM RDP session active" />
</p>

- Open **Microsoft Edge** inside the VM and go to [Wireshark.org](https://www.wireshark.org).

- Download the **Windows x64 Installer**, run the setup, and complete installation using default options.

<p align="center">
  <img src="images/an-5.jpg" width="750" alt="Downloading and installing Wireshark" />
</p>

---

<h2>📡 Step 2: Monitor ICMP Traffic Between Virtual Machines</h2>

- Launch **Wireshark** inside the Windows VM.

- From the interface list, select the active **Ethernet adapter**, then click the **shark fin icon** to begin packet capture.

<p align="center">
  <img src="images/step2-wireshark-start.png" width="750" alt="Starting packet capture in Wireshark" />
</p>

- In the **Wireshark filter bar**, type `icmp` and press **Enter** to display only ICMP packets (used by ping).

<p align="center">
  <img src="images/step2-icmp-filter.png" width="750" alt="Wireshark ICMP traffic filter" />
</p>

- In the Azure Portal, navigate to the **Linux VM**, select the **Networking** tab, and copy the **Private IP address**.

<p align="center">
  <img src="images/step2-linux-private-ip.png" width="750" alt="Linux VM private IP address in Azure" />
</p>

- Return to the Windows VM, open **PowerShell**, and run the following command:

```powershell
ping <Linux-Private-IP>
