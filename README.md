<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>


<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

Before we begin, please set up a Windows Virtual Machine in Azure. For guidance, you can refer to step 1 from my azure_network_protocols project --> [https://github.com/BrianRivera22/azure_network_protocols/]

(4 vCPU's and 8Gib memory should be sufficient)

<h2>Installation Steps</h2>

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/1.png"/>
</p>
<p>
First, within the VM (osticket-vm), download the osTicket-Installation-Files.zip --> [https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD] and unzip (extract all) this file onto your windows vm desktop. The folder should be called “osTicket-Installation-Files”

Then open to Control Panel -> Programs -> Program and Features -> Turn Windows features on or off
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/2.png"/>
</p>
<p>
Expand IIS and click World Wide Web Services -> Application Development Features -> and check the CGI box. (I expanded the files so you could see how to get there)
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/3.png"/>
</p>
<p>
Open up Internet Explorer and type into the address bar "127.0.0.1" to load the IIS page. This is the loopback address of the default webpage for the IIS. If you did this correct, it should look like the example on the right!
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/4.png"/>
</p>
<p>
Open the "osTicket-Installation-Files" from your windows vm desktop. From this file, install the PHP manager "PHPManagerForIIS_V1.5.0.msi" and then install the Rewrite Module "rewrite_amd64_en-US.msi". (see top right) 

Then, create the directory C:\PHP by going into the C drive and creating a new folder titled "PHP". (see top bottom left)

From the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 "php-7.3.8-nts-Win32-VC15-x86.zip" into the “C:\PHP” folder. (see middle)
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/5.png"/>
</p>
<p>
Going back to the “osTicket-Installation-Files” folder, install VC_redist.x86.exe. and install MySQL 5.5.62 "mysql-5.5.62-win32.msi"

For the SQL setup follow these instructions below:

Typical Setup -> Launch Configuration Wizard (after install) -> Standard Configuration -> Username: root Password: root

(BE SURE TO ENTER IN THE USERNAME AND PASSWORD CORRECTLY)
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/6.png"/>
</p>
<p>
Next, open IIS and run it as administrator. Within IIS, open the PHP manager. Then select "Register new PHP version" and enter in "C:\PHP\php-cgi.exe"
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/7.png"/>
</p>
<p>
At this point, STOP and START the IIS. From the “osTicket-Installation-Files” folder, unzip “osTicket-v1.15.8.zip” and copy the “upload” folder into “c:\inetpub\wwwroot” Within “c:\inetpub\wwwroot”, rename “upload” to “osTicket”. Once all is completed, STOP and START the IIS again.
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/8.png"/>
</p>
<p>
In the IIS, Go to sites -> Default -> osTicket On the right, click “Browse *:80”

A new site will appear on our browser. Go back to IIS, sites -> Default -> osTicket. Select osTicket and double-click PHP Manager. Click “Enable or disable an extension” Enable: "php_imap.dll" Enable: "php_intl.dll" Enable: "php_opcache.dll"

Now refresh the osTicket site in your browser.
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/9.png"/>
</p>
<p>
Now lets rename: "ost-config.php"

From: "C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php" To: "C:\inetpub\wwwroot\osTicket\include\ost-config.php"

From "ost-config.php", right click to access properties and select "Advanced". We will disable inheritance and remove all inherited permissions.
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/11.png"/>
</p>
<p>
Next, click "Add", make sure that "Write" permissions are checked. Click "Select a princpial", enter "everyone", and select "Check Names". 
BE SURE TO APPLY CHANGES
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/12.png"/>
</p>
<p>
Back in our browser, we can click continue and set up osTicket. All of the information here can be filled however you want. Do not fill it out completely, we will come back to it.
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/13.png"/>
</p>
<p>
From the “osTicket-Installation-Files” folder, install HeidiSQL. Open Heidi SQL, create a new session, enter root/root, click open and create a database called “osTicket”

Back in the browser, fill out the remaining blanks.

MySQL Database: osTicket

MySQL Username: root

MySQL Password: root

Click “Install Now!”
</p>
<br />

<p>
<img src="https://github.com/BrianRivera22/osticket_prereqs/blob/main/os%20ticket%20prereqs/14.png"/>
</p>
<p>
Congratulations! Your osTicket is now setup. Browse to your help desk login page: http://localhost/osTicket/scp/login.php
</p>
<br />
