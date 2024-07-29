# Active Directory Home Lab
![Active Directory Diagram](https://github.com/user-attachments/assets/281f36ad-957f-417d-8b24-76c265b3f693)


## Introduction

Welcome to my Home Active Directory Lab! This lab provides a hands-on experience in setting up and managing an Active Directory environment using Windows Server 2019 as a domain controller and a Windows 10 client, all within Oracle VirtualBox. This lab is an excellent opportunity for anyone interested in learning the fundamentals of Active Directory, network configuration, and virtual machine management.

In this lab, I will guide you through the essential steps to create a functional Active Directory setup. Starting with the configuration of a Windows Server 2019 virtual machine as the domain controller, we'll explore the installation and configuration of key services such as Active Directory Domain Services (AD DS) and DHCP. I will also set up NAT for internet connectivity and establish a private network for the domain.

We'll then proceed to the Windows 10 client, joining it to the domain and verifying network configurations. This lab will involve scripting with PowerShell to streamline the creation of users and groups, providing a practical approach to managing an Active Directory environment.

## Getting Started
1. Provision a Windows 2019 Server in Oracle VirtualBox 
![image](https://github.com/user-attachments/assets/2162ec51-aa6e-461e-b2a6-10f05a80996a)

2. From the Oracle VirtualBox settings, give the server two NICs. One for Network Address Translation (NAT) and one for Internal use.
![image](https://github.com/user-attachments/assets/5fd932c7-e2c1-4160-9739-c8b0c3f3fc33)
![image](https://github.com/user-attachments/assets/ebd92ca7-2481-443a-8131-abb511c9ad37)

3. Log into the Server 2019 VM with the administrator account you created during setup. Find your two NICs adn rename them. The NIC with an APIPA address (169.254.0.1) is our internal NIC. Open the IPv4 properties for the internal NIC and change the IP address to 172.16.0.1 255.255.255.0 and DNS to 172.16.0.1.
![image](https://github.com/user-attachments/assets/28b0f29f-b6ee-4c60-8dbf-41c87134f74c)

4. Install Active Directory Domain Services.
![image](https://github.com/user-attachments/assets/bf57bf75-7214-43d0-a2ee-1b0cb80f2ce8)

5. Promote this server to a Domain Controller. Choose to add a new forest and enter the name of your domain. In this lab, I will be using mydomain.com.
![image](https://github.com/user-attachments/assets/4ec32fc8-da46-4ce4-8f04-dfd3780453b1)

6. Open Active Directory Users and Computers and create a domain administrator account so that we are no longer using the built in administrator account. 
![image](https://github.com/user-attachments/assets/441b2a87-1957-4438-a70d-3954c7c3f276)

7. Log in with your domain admin account. 
![image](https://github.com/user-attachments/assets/84e444eb-0fba-4cc9-ade6-0b9db0db1abc)

8. From within server manager, select add roles and featuers and install "Remote Services"
![image](https://github.com/user-attachments/assets/36836f5d-c5b7-44b9-9bc2-754817e6af8f)

9. Still in server manager, select Tools and then click on "Routing and Remote Access". We are now going to configure NAT. Be sure to select our Internet NIC during this step. 
![image](https://github.com/user-attachments/assets/16911bff-1cbc-41b1-9f6c-b1eb68d2d694)

10. Back in server manager, install DHCP from roles and features.
![image](https://github.com/user-attachments/assets/036635de-12e8-404b-bcb9-34afe29fcc06)

11. Now we will setup our DHCP scope.
![image](https://github.com/user-attachments/assets/08a3469e-a031-4e02-9403-ee0aa44785ea)

12. Here is the Github repository that we will be getting our PowerShell script from to create our Active Directory users: https://github.com/joshmadakor1/AD_PS <br></br>

Download the zipped folder and place on it your desktop. Open PowerShell ISE as an admin. Run the command "Set-ExecutionPolicy Unrestricted" so that we are able to run scripts from the internet. Open the Create Users script. Navigate to the desktop directory where you extracted the items from the zipped folder. Now run the script. You will see all of our users being created. 

![image](https://github.com/user-attachments/assets/17df4d8a-cfe8-441a-925f-66695835857f)

<br></br>

If we look in Active Directory, we see all the users that the script created for us. 
![image](https://github.com/user-attachments/assets/42ab20e2-ba12-4bb2-a684-93dd562387e9)


13. Now it's time to create our Windows 10 Client VM. Once created, go to the Oracle VirtualBox settings and set the NIC to internal.
![image](https://github.com/user-attachments/assets/8af1712c-4b3d-4b8c-83cc-e8356b0780c8)

14. Log into the Windows 10 Client with the user account you created during setup. Join it to the domain and reboot.

![image](https://github.com/user-attachments/assets/0e328cdc-6359-44a1-8e83-0de9762dc996)


15. Log into the Windows 10 Client VM with a user account that our PowerShell script created. After logging in 

