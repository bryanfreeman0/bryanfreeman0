I begin by creating a virtual machine in azure using Windows server 2025 as the operating system. Once the machine is created I assign it a static IP of 10.0.0.4.

<img width="2214" height="1335" alt="Image" src="https://github.com/user-attachments/assets/9b047de6-bd1e-4c62-953a-35fe462bb280" />

After the VM is created I connect to it and will add a few features in the Server Manager. 
The features that I need are as follows: 
Active Directory Domain Services
DHCP Server
DNS Server

After those features are all installed I restarted the machine.

<img width="3811" height="1432" alt="Image" src="https://github.com/user-attachments/assets/4144522d-9e78-4e11-81bd-05c5d1e12387" />

After the restart I go back to the Server Manager and select the AD DS tab on the left which will give me the option to promote the server to a Domain Controller. The VM will need to restart again after this.

When the machine has restarted we can begin adding some domain users and groups. I open Active Directory Users and Groups then create the Lab1 OU for this project and then create the Computers, Users, and Groups OUs within Lab1. Once those are created I create two security groups named "IT" and "Operations". I then create three user accounts, one being myself and the other two being Bill and John Smith. I then add my account to the IT group and add the Smiths to the Operations group.

<img width="1210" height="585" alt="Image" src="https://github.com/user-attachments/assets/ed53581e-bccb-4f7e-850f-7efccdf9bdbd" />

<img width="1179" height="657" alt="Image" src="https://github.com/user-attachments/assets/b84e5bce-c3bd-4539-867e-72fdc6e6e53e" />

Now it is time to had a domain computer. For this I create a new VM in Azure in the same resource group and subnet as the previous VM that was used as the Domain Controller. Once connected to the new VM I set it's preferred DNS address to the static IP that I assigned earlier for the Domain Controller machine. Then I am able to add the VM to the domain and after a restart it appears in Active Directory Users and Computers on the Domain Controller.

<img width="1633" height="709" alt="Image" src="https://github.com/user-attachments/assets/4235ac29-99a9-445f-b1c1-6be0d6ee234c" />

Now it is time to create a few Group Po9licies. I open Group Policy Management then navigate to the Group Policy Objects section. I create two group policies, LocalAdmin and LockTaskbar. The LocalAdmin GPO assigns local admin access to members of the IT group on the domain added VM. The second GPO locks the taskbar for users of the Operations group when they log in to the domain added VM. I then link both of these GPOs to the Lab1 tree and can connect to the VM to confirm they are applied and functioning as intended.

<img width="3556" height="954" alt="Image" src="https://github.com/user-attachments/assets/988998c9-bf6b-4dd2-9127-005c8d5b1594" />
