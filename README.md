# Active Directory & Group Policy Management Lab

### Created by Drayton Rolle

---

## 📝 Project Summary

This project involved building a complete, functional Active Directory (AD) lab environment from scratch in Microsoft Azure. The primary goal was to gain hands-on experience with the fundamental tools and concepts used in enterprise IT environments for managing users, computers, and security policies.

The lab consists of a Windows Server 2019 Domain Controller and a Windows Server 2019 client machine, both configured within a private virtual network. The project covers the entire lifecycle of a basic corporate network setup: creating the domain, structuring the company into Organizational Units (OUs), managing users and groups, joining a client to the domain, and enforcing security and configuration settings through Group Policy Objects (GPOs).

This project is a practical demonstration of core skills required for Help Desk, IT Support, and Junior System Administrator roles.

---

## 🚀 Key Skills & Concepts Demonstrated

* **Cloud Infrastructure:** Deployed and managed multiple Virtual Machines and Virtual Networking components in **Microsoft Azure**.
* **Active Directory Domain Services (AD DS):** Installed and configured a new AD forest and promoted a Windows Server to a Domain Controller.
* **User & Group Management:** Created users, security groups, and Organizational Units (OUs) to mirror a corporate structure.
* **Group Policy Management:** Created, linked, and configured multiple Group Policy Objects (GPOs) to enforce security settings (restricting Control Panel access), apply branding (standardized wallpaper), and provide resources (mapping network drives).
* **DNS & Networking:** Configured client DNS settings to enable domain communication and resolved common network connectivity issues.
* **IT Troubleshooting:** Diagnosed and resolved a wide range of real-world issues, including VM resource limitations, firewall blocks, Remote Desktop protocol errors, and user permissions problems.

---

## 🛠️ Tools & Technologies Used

* **Microsoft Azure:** For creating the virtual machines and virtual network.
* **Windows Server 2019:** As the operating system for both the Domain Controller and the client machine.
* **Active Directory Users and Computers:** For managing OUs, users, and groups.
* **Group Policy Management Console:** For creating and editing GPOs.
* **Remote Desktop Protocol (RDP):** For connecting to and managing the virtual machines.

---

## 📖 Step-by-Step Project Guide

This guide provides a detailed walkthrough for replicating this project, with screenshots included at each key stage.

### Phase 0: Building the Virtual Lab in Azure

1.  **Create Resources:** In Azure, create a new Resource Group (`AD-Lab-RG`) and a Virtual Network (`AD-Lab-VNet`).
2.  **Deploy Domain Controller:** Create a `Windows Server 2019` VM named `DC-01`. Place it in the `AD-Lab-VNet`. Ensure RDP port 3389 is open.
3.  **Deploy Client Machine:** Create a second `Windows Server 2019` VM named `Client-01`. Place it in the same `AD-Lab-VNet`. Ensure RDP port 3389 is open.

    *A screenshot of the Azure portal showing both VMs in the `AD-Lab-RG` resource group.*
    `![Azure VMs](images/AD-Lab%20Resoruce%20Group.png)`

### Phase 1: Creating the Domain

1.  **Connect to DC-01:** Log in to the `DC-01` server via RDP.
2.  **Install AD DS Role:** Using Server Manager, add the "Active Directory Domain Services" role.
3.  **Promote to Domain Controller:** After installation, run the promotion wizard. Select "Add a new forest" and create a root domain (e.g., `draytontech.local`). Complete the wizard and allow the server to restart.

    *A screenshot of the successful promotion to a Domain Controller.*
    `![Promotion Success](images/Forest%20draytontech.png)`

### Phase 2: Structuring the Company in AD

1.  **Connect to DC-01:** Log in with the new domain administrator credentials (e.g., `draytontech\labadmin`).
2.  **Open ADUC:** Launch "Active Directory Users and Computers."
3.  **Create OUs, Users & Groups:** Create two OUs (`Sales`, `Marketing`), a user `jsmith` in Sales, a user `jdoe` in Marketing, and a security group `Sales-Users` containing `jsmith`.

    *A screenshot of the `jsmith` user object in Active Directory Users and Computers.*
    `![ADUC Structure](images/User%20John%20Smith.png)`

### Phase 3: Joining the Client to the Domain

1.  **Connect to Client-01:** Log in to the `Client-01` machine with its local administrator account.
2.  **Configure DNS:** Change the client's IPv4 settings to use the **Private IP address** of `DC-01` as its only DNS server.
3.  **Join Domain:** Open System Properties (`sysdm.cpl`), and on the "Computer Name" tab, change the membership from "Workgroup" to your domain (`draytontech.local`). Provide domain admin credentials when prompted. The machine will restart.

    *A screenshot of the "Welcome to the draytontech.local domain" message.*
    `![Domain Join Success](images/Welcome%20to%20draytontech.png)`

### Phase 4: Enforcing Rules with Group Policy

1.  **Connect to DC-01** and open **Group Policy Management**.
2.  **Create GPOs:** Create and link the following three GPOs:
    * `Standard Company Wallpaper` (linked to the domain)
    * `Sales Network Drive` (linked to the `Sales` OU)
    * `User Restrictions` (linked to the domain)

    *A screenshot of the Group Policy Management console showing the three GPOs linked correctly.*
    `![GPO Management](images/Rules%20with%20Group%20Policy.png)`

3.  **Edit Policies:** Configure each GPO to enforce the desired settings (desktop wallpaper, drive map, and Control Panel restriction).

### Phase 5: Verification

1.  **Log in to Client-01** as `draytontech\jsmith`.
2.  **Verify:** Check for the company wallpaper, the mapped `S:` drive, and the restriction on accessing the Control Panel.

    *A screenshot of the Client-01 desktop logged in as `jsmith`, showing the custom wallpaper and the mapped S: drive in File Explorer.*
    `![Client Verification](images/Screenshot%202025-08-15%20101828.png)`

3.  **Log out** and log in as `draytontech\jdoe` to confirm that the `S:` drive is not mapped, but the other policies apply.
