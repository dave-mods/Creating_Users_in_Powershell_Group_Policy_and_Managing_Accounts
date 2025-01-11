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

After a few minutes of the script running we can go into Active Directory Users and Computers, expand mydomain.com and look into the _EMPLOYEES folder and see all the users created so far.
![image](https://github.com/user-attachments/assets/cc1f8a46-5fc7-49e1-af8a-e4e6edde04f3)

I will pick a random user ban.sik to loginto client-1 with. and we seen in the script the password is set to Password1 for us automatically. So pick a random user and log out of client-1 and log in with the new user you picked (mydomain.com\ban.sik).
![image](https://github.com/user-attachments/assets/5d643f45-3c3a-4a12-b76a-23f060177c0b)

Logged into client-1 as your user open file exploer by clciking the folder on the bottom. Go to This PC and open the C drive. Open the Users folder. Here we see folders for everyone thats logged into this client-1 VM. We cant open these because we dont have access as a user. Now we can log out of client-1.
![image](https://github.com/user-attachments/assets/18edf686-c291-49e6-81e5-4911e2a80bba)

Now go back into our Domain Controler VM. Here we are going to setup group policy for account lockouts. Go to the search bar at the bottom type Run> gpmc.msc hit ENTER and this will bring up Group Policy Management.
![image](https://github.com/user-attachments/assets/8b37a3b8-0ed7-4d60-a430-ded2ba33e7cd)

Expand Forest: mydomain.com> Domains> mydomain.com> right click Default Domain Policy and select Edit.
![image](https://github.com/user-attachments/assets/ee554dce-afc9-4b1a-a6ef-e2545d7850a6)

In here we will expand Computer Configuration> Policies> Windows Settings> Security Settings> Account Policies and clcik Account Lockout Policy.
![image](https://github.com/user-attachments/assets/a65c1a79-1e47-4220-8f93-bd4656ba8845)

Here we will set the Account lockout duration to 30min, 5 invalid attempts, Enable, and 10min. Now we go back to Group Policy Management window and view our Defualt Domain Policy and scroll down we can see the policy's we just set in place.
![image](https://github.com/user-attachments/assets/6bf409d8-2de9-480b-97d8-e914d09a64e6)
![image](https://github.com/user-attachments/assets/179890de-a65a-41fb-b452-b466567a24b7)

So instead of waiting for the new policy to update we will login to client-1 as jane_admin and force the update so it applies right away. In client-1 search Command Promt in the bottom left search bar and open it up. We will input "gpupdate /force" and hit Enter and we will see it force the update.
![image](https://github.com/user-attachments/assets/b5c78323-5724-441d-9828-04391f6ff1fd)

Now we can log out of client-1 and log back in as our user we picked earlier. This time we will enter 6 inncorrect passwords to make sure we lock out the account.
![image](https://github.com/user-attachments/assets/5292bf2a-ff9b-4dbb-9448-e2b674bd19eb)

After we have locked out our user lets go back into our DC, into our Active Directory Users and Computers, _EMPLOYEES folder and find our user we locked out. Double click our user, go to Account and check the Unlock account box> Apply then Ok. We can now log back in to client-1 with our user and right passowrd and it will be unlocked. Mkae sure you log back out of client-1 with your user for this next step.
![image](https://github.com/user-attachments/assets/36989556-1c6e-465a-a351-eee6bd3dbccc)

Go back into the DC and we are going to go to the _EMPLOYEES folder again and Disable our user account we have been using. Highlight the users name, right click and hit Disable Account. We would do this if the employee is fired or if their account became compromised ect.
![image](https://github.com/user-attachments/assets/6beb35cc-0374-4da8-b9d3-d0ef98ffcb32)

So if we try signing back into our user account in client-1 we will get this message.
![image](https://github.com/user-attachments/assets/72697362-2981-4f20-8350-4968a394e520)

We can go back into our DC and repeat the above steps but Enable this time and sign back into client-1.
![image](https://github.com/user-attachments/assets/68b48f93-5141-458b-b8ed-0b3a807ea402)

On our DC lets view the logs of the recent events. In the search bar type in Event Viwer. In this window expand Windows Logs then click Security. Here we can see all the login's, log out's, lockout's ect along with times and names.
![image](https://github.com/user-attachments/assets/e8163650-afbe-46bc-a091-441b9277d325)

# <b>Active Directory Creating Users, Group Policy, and Managing Accounts in Azure is Now Complete<b/>
We have successfully configured Remote Desktop for non administrative users. Automated user creation with PowerShell script and managed group policies. We also covered account lockouts and log monitoring to simulate a real world IT environment.
