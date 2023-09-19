<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- 
<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Internet Information Services with CGI and Common HTTP features
- PHP Manager for IIS
- Rewrite Module
- 
- Item 5

<h2>Installation Steps</h2>

Setting up resources in Azure 
On your computer, head over to portal.azure.com and sign in 
Create a resource group 

Create a virtual machine 
- Place the virtual machine in the same resource group 
- Place the virtual machine in the same region as the resource group
- Use Windows 10 Pro Version 22h2
- Minimum of 2 virtual CPU’s and 16GB of Memory 
- Write down the login credentials

Downloading the installation files  
Go to the Azure Portal, find the public IP address of the virtual machine you just created and copy it 
Go to start, type in “Remote Desktop Connection” 
If on Mac, download Microsoft Remote Desktop app from the app store 
Paste the IP Address you copied then login with the credentials you made
Once on the virtual machine, go to Microsoft Edge, paste the link for this page into the browser and click download all on the right hand corner 
Installing IIS in Windows with CGI and Common HTTP Features 
Go to start menu of Windows > look up Control Panel > click programs > Turn Windows Features on or off 
Click Internet Information Services > Worldwide Web Services > Application Development Features > Turn on CGI

Collapse Application Development features > go to Common HTTP features > check all boxes 

To test if Internet Information Services was properly installed, go to the browser of the virtual machine and in the url, type “127.0.0.1” 
A page for Internet Information Services should pop up if all the previous steps were done correctly



Installing PHP manager for IIS  
Go to file explorer and within downloads, search for “PHPManagerForIIS_V1.5.0.msi”
Double click on it and install it

Installing Rewrite Module 
In the downloads folder of file explorer, search for “rewrite_amd64_en-US.msi”
Double click on it, a pop up will appear, accept the license agreement and install it

Creating the directory C:\PHP and installing PHP
In file explorer > find This PC > Windows (C:) > right click > New > folder > Name “PHP” 
In file explorer > go to downloads > find “php-7.3.8-nts-Win32-VC15-x86.zip”
Right click on it > extract all > click browse > This PC > Windows (C:) > Select PHP > Extract

Installing C++ Redistributable
File explorer > downloads > search for “VC_redist.x86.exe”
Double click the file > click next > click “I agree to license terms and conditions”
Install then close when finished 

Installing and setting up MYSQL Server 
File explorer > downloads > search for “mysql-5.5.62-win32.msi”
Double click on it > click next > check box agreeing with the license and terms 
Choose typical setup type > select install > check box with “Launch the MySQL Instance Configuration Wizard” 
My SQL Server Instance Configuration Wizard will display  
Check “Standard configuration” circle > click next > check “Install as Windows Service Box” > click next 
Check the box that says ‘Modify Security Settings” 
Username is “root”
Set password > retype it > click next > click execute > let it install > click finish 

Registering PHP from within IIS 
Go to start > search “Internet Information Services” > right click and run as administrator
Open PHP manager > click Register new PHP version 
A window will appear and find the ellipses(...) > click it > go to This PC > Windows (C:) > PHP folder > find “php-cgi” > open > click ok 

On IIS, find the connection tab on the left hand side, click the top of the list that has the name of your virtual machine 
You will be at the page you started at 
On the right hand of the page, under actions and manage server, click restart 

Installing osTicket 
Run two instances of file explorer 
On the first instance > downloads > find “osTicket v1.15.8” > double click
This file is zipped up, you will notice 2 folders, one called “scripts” and one called “upload”
On the second instance > This PC > Windows(C:) > inetpub > wwwroot > open the folder
With both instances of file explorer open, go back to the first instance, left click drag and drop the upload folder into the wwwroot folder
Right click and rename the upload folder exactly “osTicket” 

Go back to IIS and restart the server 
Within IIS, go to the left hand side that says “connections”, find the folder that says “sites” 
Click the arrow, click on another arrow that says “Default Web Site” then open the osTicket folder
On the folder, go the right hand side and find “Browse *:80”
A page will appear thanking you for installing osTicket which means you have done all the steps correctly
You will notice at the bottom of the page that some extensions are not enabled

Go back to IIS, go back to the osTicket page 
From there, go to PHP manager click on enable or disable extensions
Enable: php_imap.dll
Enable: php_intl.dll
Enable: php_opache.dll

-  When you go back to the web browser where you have osTicket open, you will notice the changes 

Go to file explorer > This PC > Windows(C:) > inetpub > wwwroot > osTicket > include 
Once there, find “ost-sampleconfig.php” then rename it “ost-config.php” 

Right click the same file > properties > security > advanced > disable inheritance > remove all inherited permissions from this object > go to add > select principal 

In the textbox, enter “everyone”, check names, then click ok 
Under basic permissions, check full control box and click ok 
Click apply and ok until done  
  
Go back to your web browser that has the osTicket page click continue, fill out system settings section and admin user section,
It's important to write down your login information somewhere so you don’t forget when you go to log on 

Installing HeidiSQL 
File explorer > downloads > find “Heidisql” > open 
Accept the agreement, keep clicking next and install 
Check the box that says “Launch HeidiSQL” then click finish 
When it is opened, go the bottom left side and click new 
You will need to type in your credentials from MYSQL Server, your username is root 
Click open > right click unnamed > create new > database 

Name it “osTicket” then click ok 

Go back to the osTicket page in the browser and fill out the database settings
Your MYSQL Database will be “osTicket” 
Your MYSQL Username will be “root”
Fill in your password 
Click install now 

Cleaning up 
File explorer > This PC > Windows > (C:) > inetpub > wwwroot > osTicket 
Right click setup folder and delete 
Go to include > ost-config.php > properties > right click security > advanced > click everyone > edit 
Uncheck everybox except “read & execute” and “read” 

Click ok > apply > ok > ok 

Logging into osTicket 
Go to your web browser and paste this link 
2. Then log into your credentials and you will be logged into osTicket! 
