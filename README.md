<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />






<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- osTicket
- MYSQL Server
<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)

<h2>List of Prerequisites</h2>

- Internet Information Services with CGI and Common HTTP features
- PHP Manager for IIS
- Rewrite Module
- PHP
- C++ Redistributable
- MYSQL Server
- HeidiSQL

<h2>Installation Steps</h2>

### Setting up resources in Azure 
1. On your computer, head over to portal.azure.com and sign in 
2. Create a resource group

![Screenshot (55)](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/b1f0f2d9-dfd7-4e0f-b85c-9177c1c5f1f4)

3. Create a virtual machine 
- Place the virtual machine in the same resource group 
- Place the virtual machine in the same region as the resource group
- Use Windows 10 Pro Version 22h2
- Minimum of 2 virtual CPU’s and 16GB of Memory 
- Write down the login credentials

### Downloading the installation files  
1. Go to the Azure Portal, find the public IP address of the virtual machine you just created and copy it 
2. Go to start, type in “Remote Desktop Connection” 
- If on Mac, download Microsoft Remote Desktop app from the app store 
3. Paste the IP Address you copied then login with the credentials you made
4. Once on the virtual machine, go to Microsoft Edge, paste the link for this page into the browser and click download all on the right hand corner <br>
### Installing IIS in Windows with CGI and Common HTTP Features 
1. Go to start menu of Windows > look up Control Panel > click programs > Turn Windows Features on or off 
2. Click Internet Information Services > Worldwide Web Services > Application Development Features > Turn on CGI

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/695b62d0-ea12-4b06-b6f8-e644490a483b)


3. Collapse Application Development features > go to Common HTTP features > check all boxes 

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/9d1e9bd1-1c63-4102-a99b-9609d02c1b0c)

- To test if Internet Information Services was properly installed, go to the browser of the virtual machine and in the url, type “127.0.0.1” 
- A page for Internet Information Services should pop up if all the previous steps were done correctly

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/c28130ef-1c02-4c5f-a7d3-bf472b6f798f)

### Installing PHP manager for IIS  
Go to file explorer and within downloads, search for “PHPManagerForIIS_V1.5.0.msi”
Double click on it and install it

### Installing Rewrite Module 
In the downloads folder of file explorer, search for “rewrite_amd64_en-US.msi”
Double click on it, a pop up will appear, accept the license agreement and install it

### Creating the directory C:\PHP and installing PHP
1. In file explorer > find This PC > Windows (C:) > right click > New > folder > Name “PHP” 
2. In file explorer > go to downloads > find “php-7.3.8-nts-Win32-VC15-x86.zip”
3. Right click on it > extract all > click browse > This PC > Windows (C:) > Select PHP > Extract

### Installing C++ Redistributable
1. File explorer > downloads > search for “VC_redist.x86.exe”
2. Double click the file > click next > click “I agree to license terms and conditions”
3. Install then close when finished 

### Installing and setting up MYSQL Server 
1. File explorer > downloads > search for “mysql-5.5.62-win32.msi”
2. Double click on it > click next > check box agreeing with the license and terms 
3. Choose typical setup type > select install > check box with “Launch the MySQL Instance Configuration Wizard” 
- My SQL Server Instance Configuration Wizard will display  
4. Check “Standard configuration” circle > click next > check “Install as Windows Service Box” > click next 
5. Check the box that says ‘Modify Security Settings” 
- Username is “root”
6. Set password > retype it > click next > click execute > let it install > click finish 

### Registering PHP from within IIS 
1. Go to start > search “Internet Information Services” > right click and run as administrator
2. Open PHP manager > click Register new PHP version 
3. A window will appear and find the ellipses(...) > click it > go to This PC > Windows (C:) > PHP folder > find “php-cgi” > open > click ok 

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/21e56315-e101-4e10-b8af-25d4cd2ff2a3)

4. On IIS, find the connection tab on the left hand side, click the top of the list that has the name of your virtual machine 
- You will be at the page you started at 
5. On the right hand of the page, under actions and manage server, click restart 

### Installing osTicket 
- Run two instances of file explorer 
1. On the first instance > downloads > find “osTicket v1.15.8” > double click
- This file is zipped up, you will notice 2 folders, one called “scripts” and one called “upload”
2. On the second instance > This PC > Windows(C:) > inetpub > wwwroot > open the folder
3. With both instances of file explorer open, go back to the first instance, left click drag and drop the upload folder into the wwwroot folder
4. Right click and rename the upload folder exactly “osTicket” 

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/6eac99f6-744d-4fc6-88ac-ee78ff69bb74)

5. Go back to IIS and restart the server 
6. Within IIS, go to the left hand side that says “connections”, find the folder that says “sites” 
7. Click the arrow, click on another arrow that says “Default Web Site” then open the osTicket folder
8. On the folder, go the right hand side and find “Browse *:80”
- A page will appear thanking you for installing osTicket which means you have done all the steps correctly
- You will notice at the bottom of the page that some extensions are not enabled

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/6c90c666-3ce6-4ab5-bd1f-a1725a8f0230)

9. Go back to IIS, go back to the osTicket page 
10. From there, go to PHP manager click on enable or disable extensions
- Enable: php_imap.dll
- Enable: php_intl.dll
- Enable: php_opache.dll

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/dfa333b8-cc75-479b-b97f-5d034cb82348)

- When you go back to the web browser where you have osTicket open, you will notice the changes 

11. Go to file explorer > This PC > Windows(C:) > inetpub > wwwroot > osTicket > include 
12. Once there, find “ost-sampleconfig.php” then rename it “ost-config.php” 

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/811ae2fb-11c0-42db-9801-c1bae0b9d86a)

13. Right click the same file > properties > security > advanced > disable inheritance > remove all inherited permissions from this object > go to add > select principal 

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/89835695-3a73-4783-9532-1c1b600bc457)

14. In the textbox, enter “everyone”, check names, then click ok 
15. Under basic permissions, check full control box and click ok 
16. Click apply and ok until done  
  
17. Go back to your web browser that has the osTicket page click continue, fill out system settings section and admin user section,
- It's important to write down your login information somewhere so you don’t forget when you go to log on 

### Installing HeidiSQL 
1. File explorer > downloads > find “Heidisql” > open 
2. Accept the agreement, keep clicking next and install 
3. Check the box that says “Launch HeidiSQL” then click finish 
4. When it is opened, go the bottom left side and click new 
- You will need to type in your credentials from MYSQL Server, your username is root 
5. Click open > right click unnamed > create new > database

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/bd559092-4926-4007-84db-1eaee74351ca)

6. Name it “osTicket” then click ok 

7. Go back to the osTicket page in the browser and fill out the database settings
- Your MYSQL Database will be “osTicket” 
- Your MYSQL Username will be “root”
- Fill in your password 
8. Click install now 

### Cleaning up 
1. File explorer > This PC > Windows > (C:) > inetpub > wwwroot > osTicket 
2. Right click setup folder and delete 
3. Go to include > ost-config.php > properties > right click security > advanced > click everyone > edit 
4. Uncheck everybox except “read & execute” and “read”

![image](https://github.com/adrianbautista0/osticket-prereqs/assets/142345957/7112515c-1f1f-4e5a-b867-48efca1d1514)

5. Click ok > apply > ok > ok 

Logging into osTicket 
1. Go to your web browser and paste this link 
2. Then log into your credentials and you will be logged into osTicket! 
