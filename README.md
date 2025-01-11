# Creating Users in Powershell Group Policy and Managing Accounts
![image](https://github.com/user-attachments/assets/de023c6d-fab5-452e-9223-5ce94ad72dce)

# <b>Description<b/>
This project will demonstrate how to configure Remote Desktop for non-administrative users, automate user creation with PowerShell, and manage group policies. Additionally, I’ll cover account lockouts and log monitoring to simulate a real-life IT environment. Join me as I dive deeper into deploying Active Directory and enhancing system management skills.
# <b>Environments and Utilities Used<b/>
 - Microsoft Azure
 - Virtual Machines
 - Remote Desktop Connection
 - Active Directory
# <b>Operating Systems Used<b/>
 - Windows Server
 - Windows 10
# <b>Project Walk-through<b/>
To get started lets login to client-1 VM as mydomain.com\jane_admin with the Cyberlab123! password. In the client-1 VM we will search "about your PC" in the search bar at the bottom left.
![image](https://github.com/user-attachments/assets/3927a257-78dc-443e-9417-c477be7137a4)

In here we will select Remote Desktop on the right. Go down to User Accounts. Hit Select users that can remotley access this PC. In the Remote Desktop Users box hit ADD.., in here we will put Domain Users, then check names and hit OK. Now all Domian Users by default can now login to the domain as a non admin user.
![image](https://github.com/user-attachments/assets/edf8266e-6a75-4f98-9c59-e999c73be649)

Now login to dc-1 as jane_admin if you arent still logged in. Here we will go to the search bar in bottom left and search for PowerShell ISE right clcik and open as admin.
![image](https://github.com/user-attachments/assets/780013cb-cf20-4b10-b403-e8b66bc5370d)

Open a new file and select desktop and name it create-users and save it. Then we will post our script that will generate random users and hit the green triangle (run script) button on the top bar.
![image](https://github.com/user-attachments/assets/37b34530-5472-48a3-960b-5620547af9ed)

The script will be running making all our users. We will let this run for a bit. All the users being created will be sent to the OU folder we made named _EMPLOYEES.
![image](https://github.com/user-attachments/assets/c75ebb9c-8bac-4656-94a4-a19c59a02244)

















































