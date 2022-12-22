# 42-born2beroot

<p align="center">How I did my "Born2beroot" project.</p>

<p align="center">
	<img alt="Number of lines of code" src="https://img.shields.io/tokei/lines/github/rphlr/42-born2beroot?color=green&logo=Codecademy&logoColor=green&style=flat-square">
	<img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/rphlr/42-born2beroot?color=green&logo=github&logoColor=green&style=flat-square">
	<img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/rphlr/42-born2beroot?color=green&logo=github&logoColor=green&style=flat-square">
</p> 

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# 💡 About the project

> _This project aims to help you discover the wonderful world of virtualization._

	This project is not finished yet !

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# Table of Contents
1. [**Installation step**](#installation)
	* [How to proceed](#how-to-proceed)
		* [First steps](#first-steps)
		* [ISO file installation](#iso-file-installation)
		* [VM installation](#start-the-vm)
		* [Let's  create the partitions](#lets-create-the-partitions)
			* [*The first one is the primary*](#the-first-one-is-the-primary)
			* [*The others partitions*](#the-others-partitions)
2. [**SUDO**](#sudo)
	* [Step 1: Installing *sudo*](#step-1-installing-sudo)
	* [Step 2: Adding User to *sudo* Group](#step-2-adding-user-to-sudo-group)
	* [Step 3: Running *root*-Privileged Commands](#step-3-running-root-privileged-commands)
	* [Step 4: Configuring *sudo*](#step-4-configuring-sudo)
3. [**SSH**](#ssh)
	* [Step 1: Installing & Configuring SSH](#step-1-installing--configuring-ssh)
	* [Step 2: Installing & Configuring UFW](#step-2-installing--configuring-ufw)
	* [Step 3: Connecting to Server via SSH](#step-3-connecting-to-server-via-ssh)
4. [**User Management**](#user-management)
	* [Step 1: Setting Up a Strong Password Policy](#step-1-setting-up-a-strong-password-policy)
	   * [Password Age](#password-age)
	   * [Password Strength](#password-strength)
	* [Step 2: Creating a New User](#step-2-creating-a-new-user)
	* [Step 3: Creating a New Group](#step-3-creating-a-new-group)
5. [**cron**](#cron)
	* [Setting Up a *cron* Job](#setting-up-a-cron-job)
6. [**Bonus**](#bonus)
	* [Installation](#1-installation)
	* [Linux Lighttpd MariaDB PHP *(LLMP)* Stack](#1-linux-lighttpd-mariadb-php-llmp-stack)
	   * [Step 1: Installing Lighttpd](#step-1-installing-lighttpd)
	   * [Step 2: Installing & Configuring MariaDB](#step-2-installing--configuring-mariadb)
	   * [Step 3: Installing PHP](#step-3-installing-php)
	   * [Step 4: Downloading & Configuring WordPress](#step-4-downloading--configuring-wordpress)
	   * [Step 5: Configuring Lighttpd](#step-5-configuring-lighttpd)
	* [File Transfer Protocol *(FTP)*](#2-file-transfer-protocol-ftp)
	   * [Step 1: Installing & Configuring FTP](#step-1-installing--configuring-ftp)
	   * [Step 2: Connecting to Server via FTP](#step-2-connecting-to-server-via-ftp)
7. [**Evaluation**](#evaluation)
	* [General instructions](#general-instructions)
		* [Signature file](#signature-file)
	* [Mandatory part](#mandatory-part)
		* [How does a virtual machine work?](#how-does-a-virtual-machine-work)
		* [Why Debian rather than CentOS?](#why-debian-rather-than-centos)
		* [Basic differences between Rocky and Debian?](#basic-differences-between-rocky-and-debian)
		* [The benefits of virtual machines](#the-benefits-of-virtual-machines)
		* [The difference between apt and aptitude](#the-difference-between-apt-and-aptitude)
		* [What is AppArmor?](#what-is-apparmor)
	* [Simple setup](#simple-setup)
		* [Check if UFW is started](#check-if-ufw-is-started)
		* [Check if SSH is started](#check-if-ssh-is-started)
	* [**User**](#user)
		* [Check if user is in the sudo and user42 group](#check-if-user-is-in-the-sudo-and-the-user42-group)
		* [Add a new user](#add-a-new-user)
		* [Create the `evaluating` group](#create-the-evaluating-group)
		* [Add user to the group](#add-user-to-the-group)
		* [Advantages and disadvantages of this password policy](#advantages-and-disadvantages-of-this-password-policy)
	* [Hostname and partitions](#hostname-and-partitions)
		* [Change the hostname](#change-the-hostname)
		* [Check partitions](#check-partitions)
		* [What is LVM and what it is all about ?](#what-is-lvm-and-what-it-is-all-about)
	* [SUDO](#sudo-1)
		* [Check if sudo is properly installed](#check-if-sudo-is-properly-installed)
		* [Assign an user to sudo group](#assign-an-user-to-sudo-group)
		* [Check sudo settings](#check-sudo-settings)
			* [*Strict rules*](#strict-rules)
			* [*Verify the logs*](#verify-the-logs)
	* [UFW / Firewall](#ufw--firewall)
		* [Check UFW status and ports](#check-ufw-status-and-ports)
			* [*Add a new rule*](#add-a-new-rule)
			* [*Delete a rule*](#delete-a-rule)
	* [SSH](#ssh-1)
		* [Check SSH status](#check-ssh-status)
		* [List open SSH ports](#list-open-ssh-ports)
	* [Script monitoring](#script-monitoring)
		* [How does the script work ?](#how-does-the-script-works)
		* [What "cron" is ?](#what-is-cron)
	* [Bonus](#bonus-1)
		* [WordPress site](#wordpress-site)
		* [FTP service](#ftp-service)

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# **Installation**

At the time of writing, the latest stable version of [Debian](https://www.debian.org) is *Debian 11 Bullseye*.
You can download the latest *netinst* debian image (a small CD image that contains just the core Debian installer code and a small core set of text-mode programs) [here](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/).

## How to proceed

I've done the bonus parts too.

### First steps

First, let's create a new virtual machine.
![how-to-proceed_image](how-to-proceed_images/0001.png)

Install it in you folder in the "sgoinfre" for having it on any computer of the school or "goinfre" for local (much faster).
![how-to-proceed_image](how-to-proceed_images/0002.png)

Let the memory size as default.
![how-to-proceed_image](how-to-proceed_images/0003.png)

Create a virtual hard disk.
![how-to-proceed_image](how-to-proceed_images/0004.png)

Choose VirtualBox Disk Image.
![how-to-proceed_image](how-to-proceed_images/0005.png)

Choose dynamically allocated.
![how-to-proceed_image](how-to-proceed_images/0006.png)

Choose the size of your VM (I let 12GB) and create it.
![how-to-proceed_image](how-to-proceed_images/0007.png)

Click on settings button
![how-to-proceed_image](how-to-proceed_images/0008.png)

### ISO file installation

Click on storage.
![how-to-proceed_image](how-to-proceed_images/0009.png)

Click on the empty controller and the disk icon and follow theses steps.
![how-to-proceed_image](how-to-proceed_images/0010.png)

![how-to-proceed_image](how-to-proceed_images/0011.png)

![how-to-proceed_image](how-to-proceed_images/0012.png)

![how-to-proceed_image](how-to-proceed_images/0013.png)

![how-to-proceed_image](how-to-proceed_images/0014.png)

### Start the VM

![how-to-proceed_image](how-to-proceed_images/0015.png)

![how-to-proceed_image](how-to-proceed_images/0016.png)

You can scale the windows for having it a little bit bigger.
![how-to-proceed_image](how-to-proceed_images/0017.png)

Follow theses steps for the installation with bonuses (you can [contact me](mailto:rrouille@student.42lausanne.ch) if you still have some question to how to proceed).
![how-to-proceed_image](how-to-proceed_images/0018.png)

![how-to-proceed_image](how-to-proceed_images/0019.png)

![how-to-proceed_image](how-to-proceed_images/0020.png)

![how-to-proceed_image](how-to-proceed_images/0021.png)

![how-to-proceed_image](how-to-proceed_images/0022.png)

![how-to-proceed_image](how-to-proceed_images/0023.png)

![how-to-proceed_image](how-to-proceed_images/0024.png)

![how-to-proceed_image](how-to-proceed_images/0025.png)

![how-to-proceed_image](how-to-proceed_images/0026.png)

![how-to-proceed_image](how-to-proceed_images/0027.png)

![how-to-proceed_image](how-to-proceed_images/0028.png)

![how-to-proceed_image](how-to-proceed_images/0029.png)

![how-to-proceed_image](how-to-proceed_images/0030.png)

### Let's  create the partitions

The size may change.

#### *The first one is the primary*

![how-to-proceed_image](how-to-proceed_images/0031.png)

![how-to-proceed_image](how-to-proceed_images/0032.png)

![how-to-proceed_image](how-to-proceed_images/0033.png)

![how-to-proceed_image](how-to-proceed_images/0034.png)

![how-to-proceed_image](how-to-proceed_images/0035.png)

![how-to-proceed_image](how-to-proceed_images/0036.png)

![how-to-proceed_image](how-to-proceed_images/0037.png)

![how-to-proceed_image](how-to-proceed_images/0038.png)

Be sure to mount it to the boot partition.

![how-to-proceed_image](how-to-proceed_images/0039.png)

![how-to-proceed_image](how-to-proceed_images/0040.png)

![how-to-proceed_image](how-to-proceed_images/0041.png)

#### *The others partitions*

![how-to-proceed_image](how-to-proceed_images/0042.png)

![how-to-proceed_image](how-to-proceed_images/0043.png)

![how-to-proceed_image](how-to-proceed_images/0044.png)

![how-to-proceed_image](how-to-proceed_images/0045.png)

![how-to-proceed_image](how-to-proceed_images/0046.png)

![how-to-proceed_image](how-to-proceed_images/0047.png)

![how-to-proceed_image](how-to-proceed_images/0048.png)

Encrypt the disk.

![how-to-proceed_image](how-to-proceed_images/0049.png)

![how-to-proceed_image](how-to-proceed_images/0050.png)

![how-to-proceed_image](how-to-proceed_images/0051.png)

![how-to-proceed_image](how-to-proceed_images/0052.png)

![how-to-proceed_image](how-to-proceed_images/0052a.png)

![how-to-proceed_image](how-to-proceed_images/0053.png)

![how-to-proceed_image](how-to-proceed_images/0054.png)

![how-to-proceed_image](how-to-proceed_images/0055.png)

![how-to-proceed_image](how-to-proceed_images/0056.png)

![how-to-proceed_image](how-to-proceed_images/0057.png)

![how-to-proceed_image](how-to-proceed_images/0058.png)

![how-to-proceed_image](how-to-proceed_images/0059.png)

![how-to-proceed_image](how-to-proceed_images/0060.png)

![how-to-proceed_image](how-to-proceed_images/0061.png)

![how-to-proceed_image](how-to-proceed_images/0062.png)

![how-to-proceed_image](how-to-proceed_images/0063.png)

![how-to-proceed_image](how-to-proceed_images/0064.png)

![how-to-proceed_image](how-to-proceed_images/0065.png)

![how-to-proceed_image](how-to-proceed_images/0066.png)

![how-to-proceed_image](how-to-proceed_images/0067.png)

![how-to-proceed_image](how-to-proceed_images/0068.png)

![how-to-proceed_image](how-to-proceed_images/0069.png)

![how-to-proceed_image](how-to-proceed_images/0070.png)

![how-to-proceed_image](how-to-proceed_images/0071.png)

![how-to-proceed_image](how-to-proceed_images/0072.png)

![how-to-proceed_image](how-to-proceed_images/0073.png)

![how-to-proceed_image](how-to-proceed_images/0074.png)

![how-to-proceed_image](how-to-proceed_images/0075.png)

![how-to-proceed_image](how-to-proceed_images/0076.png)

![how-to-proceed_image](how-to-proceed_images/0077.png)

![how-to-proceed_image](how-to-proceed_images/0078.png)

![how-to-proceed_image](how-to-proceed_images/0079.png)

![how-to-proceed_image](how-to-proceed_images/0080.png)

![how-to-proceed_image](how-to-proceed_images/0081.png)

![how-to-proceed_image](how-to-proceed_images/0082.png)

![how-to-proceed_image](how-to-proceed_images/0083.png)

![how-to-proceed_image](how-to-proceed_images/0084.png)

![how-to-proceed_image](how-to-proceed_images/0085.png)

![how-to-proceed_image](how-to-proceed_images/0086.png)

Here is a tricks for the "var--log" partition. We need to put only one hyphen because it will be doubled after !

![how-to-proceed_image](how-to-proceed_images/0087.png)

![how-to-proceed_image](how-to-proceed_images/0088.png)

![how-to-proceed_image](how-to-proceed_images/0089.png)

![how-to-proceed_image](how-to-proceed_images/0090.png)

![how-to-proceed_image](how-to-proceed_images/0091.png)

![how-to-proceed_image](how-to-proceed_images/0092.png)

![how-to-proceed_image](how-to-proceed_images/0093.png)

![how-to-proceed_image](how-to-proceed_images/0094.png)

![how-to-proceed_image](how-to-proceed_images/0095.png)

![how-to-proceed_image](how-to-proceed_images/0096.png)

![how-to-proceed_image](how-to-proceed_images/0097.png)

![how-to-proceed_image](how-to-proceed_images/0098.png)

![how-to-proceed_image](how-to-proceed_images/0099.png)

![how-to-proceed_image](how-to-proceed_images/0100.png)

![how-to-proceed_image](how-to-proceed_images/0101.png)

![how-to-proceed_image](how-to-proceed_images/0102.png)

![how-to-proceed_image](how-to-proceed_images/0103.png)

![how-to-proceed_image](how-to-proceed_images/0104.png)

![how-to-proceed_image](how-to-proceed_images/0105.png)

![how-to-proceed_image](how-to-proceed_images/0106.png)

![how-to-proceed_image](how-to-proceed_images/0107.png)

![how-to-proceed_image](how-to-proceed_images/0108.png)

![how-to-proceed_image](how-to-proceed_images/0109.png)

![how-to-proceed_image](how-to-proceed_images/0110.png)

![how-to-proceed_image](how-to-proceed_images/0111.png)

![how-to-proceed_image](how-to-proceed_images/0112.png)

![how-to-proceed_image](how-to-proceed_images/0113.png)

![how-to-proceed_image](how-to-proceed_images/0114.png)

![how-to-proceed_image](how-to-proceed_images/0115.png)

![how-to-proceed_image](how-to-proceed_images/0116.png)

![how-to-proceed_image](how-to-proceed_images/0117.png)

![how-to-proceed_image](how-to-proceed_images/0118.png)

![how-to-proceed_image](how-to-proceed_images/0119.png)

![how-to-proceed_image](how-to-proceed_images/0120.png)

![how-to-proceed_image](how-to-proceed_images/0121.png)

![how-to-proceed_image](how-to-proceed_images/0122.png)

![how-to-proceed_image](how-to-proceed_images/0123.png)

![how-to-proceed_image](how-to-proceed_images/0124.png)

![how-to-proceed_image](how-to-proceed_images/0125.png)

![how-to-proceed_image](how-to-proceed_images/0126.png)

![how-to-proceed_image](how-to-proceed_images/0127.png)

![how-to-proceed_image](how-to-proceed_images/0128.png)

![how-to-proceed_image](how-to-proceed_images/0129.png)

![how-to-proceed_image](how-to-proceed_images/0130.png)

![how-to-proceed_image](how-to-proceed_images/0131.png)

![how-to-proceed_image](how-to-proceed_images/0132.png)

![how-to-proceed_image](how-to-proceed_images/0133.png)

![how-to-proceed_image](how-to-proceed_images/0134.png)

![how-to-proceed_image](how-to-proceed_images/0135.png)

![how-to-proceed_image](how-to-proceed_images/0136.png)

![how-to-proceed_image](how-to-proceed_images/0137.png)

![how-to-proceed_image](how-to-proceed_images/0138.png)

![how-to-proceed_image](how-to-proceed_images/0139.png)

![how-to-proceed_image](how-to-proceed_images/0140.png)

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# And the result is :

![how-to-proceed_image](how-to-proceed_images/0141.png)

Don't forget to save a snapshot after this step to save the machine.

![how-to-proceed_image](how-to-proceed_images/0142.png)

![how-to-proceed_image](how-to-proceed_images/0143.png)

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# **SUDO**

## Step 1: Installing *sudo*

Switch to *root* and its environment.
```
$ su -
Password:
```
Install *sudo*.
```
$ apt install sudo
```
Verify whether *sudo* was successfully installed
```
$ dpkg -l | grep sudo
```

## Step 2: Adding User to *sudo* Group

Add user to *sudo* group.
```
$ adduser <username> sudo
```
Alternatively, add user to *sudo* group.
```
$ usermod -aG sudo <username>
```
Verify whether user was successfully added to *sudo* group.
```
$ getent group sudo
```
Reboot for changes to take effect, then log in and verify *sudopowers*.
```
$ reboot
<--->
Debian GNU/Linux 10 <hostname> tty1

<hostname> login: <username>
Password: <password>
<--->
$ sudo -v
[sudo] password for <username>: <password>
```

## Step 3: Running *root*-Privileged Commands

From here on out, run *root*-privileged commands via prefix `sudo`. For instance:
```
$ sudo apt update
```

## Step 4: Configuring *sudo*

Configure *sudo* via `sudo nano /etc/sudoers.d/<filename>`. `<filename>` shall not end in `~` or contain `.`.
```
$ sudo nano /etc/sudoers.d/<filename>
```
To limit authentication using *sudo* to 3 attempts *(defaults to 3 anyway)* in the event of an incorrect password, add below line to the file.
```
Defaults        passwd_tries=3
```
To add a custom error message in the event of an incorrect password:
```
Defaults        badpass_message="<custom-error-message>"
```

To log all *sudo* commands to `/var/log/sudo/<filename>`:
```
$ sudo mkdir /var/log/sudo
<~~~>
Defaults        logfile="/var/log/sudo/<filename>"
<~~~>
```
To archive all *sudo* inputs & outputs to `/var/log/sudo/`:
```
Defaults        log_input,log_output
Defaults        iolog_dir="/var/log/sudo"
```
To require *TTY*:
```
Defaults        requiretty
```
To set *sudo* paths to `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin`:
```
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# **SSH**

## Step 1: Installing & Configuring SSH

Install *openssh-server*.
```
$ sudo apt install openssh-server
```
Verify whether *openssh-server* was successfully installed.
```
$ dpkg -l | grep ssh
```
Configure SSH.
```
$ sudo nano /etc/ssh/sshd_config
```
To set up SSH using Port 4242, replace below line:
```
#Port 22
```
with:
```
Port 4242
```
To disable SSH login as *root* irregardless of authentication mechanism, replace below line
```
#PermitRootLogin prohibit-password
```
with:
```
PermitRootLogin no
```
Check SSH status.
```
$ sudo service ssh status
```
Alternatively, check SSH status.
```
$ systemctl status ssh
```

## Step 2: Installing & Configuring UFW

Install *ufw*.
```
$ sudo apt install ufw
```
Verify whether *ufw* was successfully installed.
```
$ dpkg -l | grep ufw
```
Enable Firewall.
```
$ sudo ufw enable
```
Allow incoming connections using Port 4242.
```
$ sudo ufw allow 4242
```
Check UFW status.
```
$ sudo ufw status
```

Don't forget to open ports in you virtual machine
zzzzzzzzIMAGE ICIzzzzzzzz

## Step 3: Connecting to Server via SSH

SSH into your virtual machine using Port 4242.
```
$ ssh <username>@<ip-address> -p 4242
```
Terminate SSH session at any time.
```
$ logout
```
Alternatively, terminate SSH session.
```
$ exit
```

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# **User Management**

## Step 1: Setting Up a Strong Password Policy

### Password Age

Configure password age policy.
```
$ sudo nano /etc/login.defs
```
To set password to expire every 30 days, replace below line
```
PASS_MAX_DAYS   99999
```
with:
```
PASS_MAX_DAYS   30
```
To set minimum number of days between password changes to 2 days, replace below line
```
PASS_MIN_DAYS   0
```
with:
```
PASS_MIN_DAYS   2
```
To send user a warning message 7 days *(defaults to 7 anyway)* before password expiry, keep below line as is.
```
PASS_WARN_AGE   7
```

### Password Strength

Secondly, to set up policies in relation to password strength, install the *libpam-pwquality* package.
```
$ sudo apt install libpam-pwquality
```
Verify whether *libpam-pwquality* was successfully installed.
```
$ dpkg -l | grep libpam-pwquality
```
Configure password strength policy, specifically the below line:
```
$ sudo nano /etc/pam.d/common-password
<~~~>
password        requisite                       pam_pwquality.so retry=3
<~~~>
```
To set password minimum length to 10 characters, add below option to the above line.
```
minlen=10
```
To require password to contain at least an uppercase character and a numeric character:
```
ucredit=-1 dcredit=-1
```
To set a maximum of 3 consecutive identical characters:
```
maxrepeat=3
```
To reject the password if it contains `<username>` in some form:
```
reject_username
```
To set the number of changes required in the new password from the old password to 7:
```
difok=7
```
To implement the same policy on *root*:
```
enforce_for_root
```
Finally, it should look like the below:
```
password        requisite                       pam_pwquality.so retry=3 minlen=10 ucredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root
```

## Step 2: Creating a New User

Create new user.
```
$ sudo adduser <username>
```
Verify whether user was successfully created.
```
$ getent passwd <username>
```
Verify newly-created user's password expiry information.
```
$ sudo chage -l <username>
Last password change								: <last-password-change-date>
Password expires									: <last-password-change-date + PASS_MAX_DAYS>
Password inactive									: never
Account expires										: never
Minimum number of days between password change		: <PASS_MIN_DAYS>
Maximum number of days between password change		: <PASS_MAX_DAYS>
Number of days of warning before password expires	: <PASS_WARN_AGE>
```

## Step 3: Creating a New Group

Create new *user42* group.
```
$ sudo addgroup user42
```
Add user to *user42* group.
```
$ sudo adduser <username> user42
```
Alternatively, add user to *user42* group.
```
$ sudo usermod -aG user42 <username>
```
Verify whether user was successfully added to *user42* group.
```
$ getent group user42
```

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# **cron**

## Setting Up a *cron* Job

Configure *cron* as *root*.
```
$ sudo crontab -u root -e
```
To schedule a shell script to run every 10 minutes, replace add line.
```
*/10 * * * * sh /path/to/script
```
Check *root*'s scheduled *cron* jobs.
```
$ sudo crontab -u root -l
```

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# **Bonus**

## #1: Linux Lighttpd MariaDB PHP *(LLMP)* Stack

### Step 1: Installing Lighttpd

Install *lighttpd*.
```
$ sudo apt install lighttpd
```
Verify whether *lighttpd* was successfully installed.
```
$ dpkg -l | grep lighttpd
```
Allow incoming connections using Port 80.
```
$ sudo ufw allow 80
```

### Step 2: Installing & Configuring MariaDB

Install *mariadb-server*.
```
$ sudo apt install mariadb-server
```
Verify whether *mariadb-server* was successfully installed.
```
$ dpkg -l | grep mariadb-server
```
Start interactive script to remove insecure default settings.
```
$ sudo mysql_secure_installation
Enter current password for root (enter for none): #Just press Enter (do not confuse database root with system root)
Switch to unix_socket authentification [Y/n] n
Set root password? [Y/n] n
Remove anonymous users? [Y/n] Y
Disallow root login remotely? [Y/n] Y
Remove test database and access to it? [Y/n] Y
Reload privilege tables now? [Y/n] Y
```
Log in to the MariaDB console.
```
$ sudo mariadb
MariaDB [(none)]>
```
Create new database.
```
MariaDB [(none)]> CREATE DATABASE <database-name>;
```
Create new database user and grant them full privileges on the newly-created database.
```
MariaDB [(none)]> GRANT ALL ON <database-name>.* TO '<username-2>'@'localhost' IDENTIFIED BY '<password-2>' WITH GRANT OPTION;
```
Flush the privileges.
```
MariaDB [(none)]> FLUSH PRIVILEGES;
```
Exit the MariaDB shell.
```
MariaDB [(none)]> exit
```
Verify whether database user was successfully created by logging in to the MariaDB console.
```
$ mariadb -u <username-2> -p
Enter password: <password-2>
MariaDB [(none)]>
```
Confirm whether database user has access to the database.
```
MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| <database-name>    |
+--------------------+
```
Exit the MariaDB shell.
```
MariaDB [(none)]> exit
```

### Step 3: Installing PHP

Install *php-cgi* & *php-mysql*.
```
$ sudo apt install php-cgi php-mysql
```
Verify whether *php-cgi* & *php-mysql* was successfully installed.
```
$ dpkg -l | grep php
```

### Step 4: Downloading & Configuring WordPress

Install *wget*.
```
$ sudo apt install wget
```
Download WordPress to `/var/www/html`.
```
$ sudo wget http://wordpress.org/latest.tar.gz -P /var/www/html
```
Extract downloaded content.
```
$ sudo tar -xzvf /var/www/html/latest.tar.gz
```
Remove tarball.
```
$ sudo rm /var/www/html/latest.tar.gz
```
Copy content of `wordpress` to `/var/www/html`.
```
$ sudo cp -r wordpress/* /var/www/html
```
Remove `wordpress`.
```
$ sudo rm -rf wordpress
```
Create WordPress configuration file from its sample.
```
$ sudo cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
```
Configure WordPress to reference previously-created MariaDB database & user.
```
$ sudo nano /var/www/html/wp-config.php
```
Replace the below
```
define( 'DB_NAME', 'database_name_here' );^M
define( 'DB_USER', 'username_here' );^M
define( 'DB_PASSWORD', 'password_here' );^M
```
with:
```
define( 'DB_NAME', '<database-name>' );^M
define( 'DB_USER', '<username-2>' );^M
define( 'DB_PASSWORD', '<password-2>' );^M
```

### Step 5: Configuring Lighttpd

Enable below modules.
```
$ sudo lighty-enable-mod fastcgi
$ sudo lighty-enable-mod fastcgi-php
$ sudo service lighttpd force-reload
```

### Step 6: Install Wordpress

Go on your browser, enter localhost or 127.0.0.1 on the URL bar and name you site, add a password and an email and click on 'Install WordPress'.


![how-to-proceed_image](how-to-proceed_images/0144.png)

Now click on 'Log in'.

![how-to-proceed_image](how-to-proceed_images/0145.png)

Your WordPress is installed, well done ! Now you can configure it.

![how-to-proceed_image](how-to-proceed_images/0146.png)

## #2: File Transfer Protocol *(FTP)*

### Step 1: Installing & Configuring FTP

Install FTP.
```
$ sudo apt install vsftpd
```
Verify whether *vsftpd* was successfully installed.
```
$ dpkg -l | grep vsftpd
```
Allow incoming connections using Port 21.
```
$ sudo ufw allow 21
```
Configure *vsftpd*.
```
$ sudo nano /etc/vsftpd.conf
```
To enable any form of FTP write command, uncomment below line:
```
#write_enable=YES
```
To set root folder for FTP-connected user to `/home/<username>/ftp`, add below lines:
```
$ sudo mkdir /home/<username>/ftp
$ sudo mkdir /home/<username>/ftp/files
$ sudo chown nobody:nogroup /home/<username>/ftp
$ sudo chmod a-w /home/<username>/ftp
<~~~>
user_sub_token=$USER
local_root=/home/$USER/ftp
<~~~>
```
To prevent user from accessing files or using commands outside the directory tree, uncomment below line:
```
#chroot_local_user=YES
```
To whitelist FTP, add below lines:
```
$ sudo nano /etc/vsftpd.userlist
$ echo <username> | sudo tee -a /etc/vsftpd.userlist
<~~~>
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
<~~~>
```

### Step 2: Connecting to Server via FTP

FTP into your virtual machine.
```
$ ftp <ip-address>
```
Terminate FTP session at any time.

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# **Evaluation**

Take a look at the evaluation questions here : PDF

Here is some help for you :

## General instructions

### Signature file

## Mandatory part

### How does a virtual machine work?

A virtual machine (VM) is software that simulates the existence of a physical machine. It allows a computer to run multiple operating systems (OS) and software at the same time, each in its own VM.

Here is how a virtual machine generally works:

1. The host computer runs the virtual machine software, which creates one or more VMs.
2. Each VM is configured with a number of resources, such as memory, processors, and virtual disks.
3. The virtual machine software installs an operating system and any necessary software in each VM.
4. Users can access the VMs and run programs on them as if they were using a dedicated physical computer.

The virtual machine software acts as an intermediary layer between the host computer's hardware and the VMs, translating instructions sent to the VMs into instructions that the host computer's hardware can understand. This allows the VMs to function as independent computers, but sharing the host computer's resources.

Virtual machines are commonly used to run software that is not compatible with the host computer's operating system, or to isolate different work environments. They are also often used in cloud computing, where they allow for easy deployment of new instances of software or operating systems without having to purchase new hardware.

### Why Debian rather than CentOS?

Debian and CentOS are both Linux operating systems, but they differ in important ways that may make one a more advantageous choice for some users.

A key difference between the two is that Debian is a community-driven project, while CentOS is developed by Red Hat. This means that Debian is developed and maintained by a group of volunteers, while CentOS is developed and maintained by a professional company.

Debian is known for its stability and reliability, as well as its large repository of pre-compiled software packages. It is a popular choice for servers and other production environments, as well as for use on personal computers.

CentOS, on the other hand, is based on Red Hat Enterprise Linux (RHEL) and is designed to be compatible with RHEL. It is often used in enterprise environments, as it is well-suited for running critical applications and is known for its security and stability.

### Basic differences between Rocky and Debian?

Rocky Linux is a new Linux distribution that is based on CentOS and designed to be a direct alternative to CentOS. It was created in response to concerns about the future of CentOS, which is no longer developed by Red Hat.

A key difference between Rocky Linux and Debian is that Rocky Linux is based on CentOS, which is itself based on Red Hat Enterprise Linux (RHEL). Debian, on the other hand, is an independent distribution that is not based on any other distribution.

Another difference is that Rocky Linux focuses on providing a stable and reliable platform for enterprise users, while Debian is more broadly focused on providing a stable and reliable operating system for a wide range of users, including personal users, servers, and other production environments.

In terms of software packages, Rocky Linux includes many packages similar to those in CentOS, as well as additional packages from other sources. Debian has a larger repository of pre-compiled software packages, with a focus on free and open source software.

Overall, the main difference between Rocky Linux and Debian is that Rocky Linux is designed to be an alternative to CentOS, while Debian is a standalone distribution with its own development philosophy and community.

### The benefits of virtual machines

Virtual machines are computer programs that allow a computer to run multiple operating systems concurrently. They create a simulated environment on a single physical machine, in which each virtual machine acts as a separate computer with its own operating system, processor, memory, and storage.

There are several reasons someone might use a virtual machine:

1. Testing and development: Virtual machines allow developers to test their software on different operating systems and configurations without having to purchase multiple physical machines.
2. Isolation and security: Virtual machines can be used to isolate certain tasks or applications from the host operating system, which can be useful for security reasons. For example, if you need to run a potentially malicious application, you can do so in a virtual machine, which will contain any damage the application might cause.
3. Resource allocation: Virtual machines allow you to allocate resources (such as CPU, memory, and storage) to each virtual machine as needed, which can be helpful if you have limited physical resources.
4. Compatibility: If you need to run an outdated application that is not compatible with your current operating system, you can use a virtual machine to run the application in an older operating system.

Overall, virtual machines offer a flexible and cost-effective solution for running multiple operating systems and applications on a single physical machine.

### The difference between apt and aptitude

`apt` is a package management program for Debian and its derivatives, such as Ubuntu. It allows for installing, updating, and managing software packages on a system that uses the Debian package management system (dpkg). `apt` stands for "Advanced Packaging Tool".

`aptitude` is also a package management program for Debian and its derivatives, but it uses a different text-mode interface from `apt`. `aptitude` stands for "Advanced Packaging Tool Interface".

Generally, both `apt` and `aptitude` are used to manage software packages on a Debian-based system, but they have slightly different commands and syntax. For example, to update the list of available packages with `apt`, you can use the command `apt update`, while to update the list of packages with `aptitude`, you can use the command `aptitude update`.

It is worth noting that `aptitude` is considered more advanced than `apt`, as it is able to automatically resolve dependencies and conflicts when installing or removing packages. However, `apt` is often faster and easier to use than `aptitude`, as it has a simpler interface and more concise syntax.

### What is AppArmor?

AppArmor (Application Armor) is a security system that allows for limiting the privileges and actions of a program or process on a Linux system. It is a kind of "firewall" that protects the system by limiting the actions of a program to those that are explicitly allowed by the security policy defined for that program.

AppArmor is primarily used to protect systems against malicious programs and spyware, but it can also be used to limit the actions of a legitimate program that may be misused or to limit programming errors that could compromise the security of the system.

AppArmor is built into some Linux distributions, such as Ubuntu, and can be enabled and configured using special configuration files called "AppArmor profiles". These profiles define the allowed actions for each program and can be modified to tailor the security rules to your specific needs.

## Simple setup

### Check if UFW is started

```bash
$ sudo ufw status
```

### Check if SSH is started

```bash
$ sudo service ssh status
```

## User

### Check if user is in the `sudo` and the `user42` group

```bash
$ groups <user>
```

### Add a new user

```bash
$ sudo adduser <username>
```

Verify whether user was successfully created.

```bash
$ getent passwd <username>
```

### Create the `evaluating` group

```bash
$ sudo addgroup evaluating
```

### Add user to the group

```bash
$ sudo adduser <username> evaluating
```

You can also add the user to the group like this:

```bash
$ sudo usermod -aG evaluating <username>
```

### Advantages and disadvantages of this password policy

### Check if user has been added to the `evaluating` group

```bash
$ getent group evaluating
```

### Delete a user

```bash
$ sudo userdel -r <user>
```

### Delete a group

```bash
$ sudo groupdel <group>
```

## Hostname and partitions

### Change the hostname

```bash
$ sudo hostnamectl set-hostname mon-nom-de-machine
```

Check if the hostname has changed without restarting.

```bash
$ hostname
```

Don't forget to restart the machine.

```bash
$ sudo reboot
```

### Check partitions

```bash
$ lsblk
```

### What is LVM and what it is all about ?

Logical Volume Manager (LVM) is a system for managing disk storage space on Linux systems. It allows you to create logical volumes, which are virtual partitions that can span across multiple physical disks or partitions. This can be useful in a number of situations, such as when you want to create a large logical volume from multiple smaller disks, or when you want to easily resize a volume without having to repartition the disk.

LVM works by creating a volume group (VG), which is a collection of physical disks or partitions that can be used to create logical volumes. Each logical volume is then treated as a separate block device, just like a traditional disk partition. This allows you to use LVM to manage your disk space in a more flexible and dynamic way.

Some of the main benefits of using LVM include:

The ability to easily resize logical volumes without having to repartition the disk.

The ability to create logical volumes that span across multiple physical disks or partitions, allowing you to use all of your available disk space more efficiently.

The ability to easily add or remove physical disks from a volume group without having to reconfigure your disk partitions.

The ability to create snapshot copies of logical volumes, which can be used for backup or testing purposes.

LVM is a powerful tool that can be used to manage your disk space in a more flexible and dynamic way. It is widely used on Linux systems and is an important part of many system administrator's toolkit.

## SUDO

### Check if sudo is properly installed

```bash
$ dpkg -l | grep sudo
```

### Assign an user to sudo group

```bash
$ sudo usermod -aG sudo <username>
```

### What is TTY?

"TTY" is an acronym for "teletype", which refers to a computer's terminal interface. When using the **`sudo`** command, you may see the **`-t`** option followed by a TTY number, for example **`-t 1`**.

This option allows you to specify which terminal the **`sudo`** command should be run on. By default, the **`sudo`** command is run on the current terminal (the one you are currently on).

Here is an example of using the **`-t`** option with the **`sudo`** command:

```bash
$ sudo -t 1 commande
```

In this example, the **command** will be run on terminal 1.

It is important to note that the **`-t`** option is not required and is generally not used in most cases. It can be useful in certain situations, for example when you want to run a **`sudo`** command on a specific terminal.

### Check sudo settings

```bash
$ sudo visudo
```

#### *Strict rules*

#### *Verify the logs*

## UFW / Firewall

### Check UFW status and ports

```bash
$ sudo ufw status
```

#### *Add a new rule.*

```bash
$ sudo ufw allow 8080
```

#### *Delete a rule.*

```bash
$ sudo ufw delete <rule_number>
```

## SSH

### Check SSH status

```bash
$ sudo service ssh status
```

It can also be done this way:

```bash
$ systemctl status ssh
```

### What is SSH?

Secure Shell (SSH) is a network protocol that allows you to remotely connect to a computer and send it commands remotely. It is commonly used to access remote servers or computers in a secure and encrypted manner, using an encrypted connection.

SSH is widely used to administer remote servers and computers, as well as to transfer files between computers. It is also commonly used to establish a remote connection to a computer in order to run commands and use applications as if you were in front of the computer in question.

To use SSH, you need an SSH client on your local computer and an SSH server on the remote computer you want to connect to. There are many available SSH clients and servers for different platforms, including Linux, macOS, and Windows.

### List open SSH ports

```bash
$ sudo nano /etc/ssh/sshd_config
```

## Script monitoring

```bash
#!/bin/bash
arc=$(uname -a)
pcpu=$(grep "physical id" /proc/cpuinfo | sort | uniq | wc -l)
vcpu=$(grep "^processor" /proc/cpuinfo | wc -l)
fram=$(free -m | awk '$1 == "Mem:" {print $2}')
uram=$(free -m | awk '$1 == "Mem:" {print $3}')
pram=$(free | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')
fdisk=$(df -Bg | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $2} END {print ft}')
udisk=$(df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}')
pdisk=$(df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} {ft+= $2} END {printf("%d"), ut/ft*100}')
cpul=$(top -bn1 | grep '^%Cpu' | cut -c 9- | xargs | awk '{printf("%.1f%%"), $1 + $3}')
lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')
lvmt=$(lsblk | grep "lvm" | wc -l)
lvmu=$(if [ $lvmt -eq 0 ]; then echo no; else echo yes; fi)
#You need to install net tools for the next step [$ sudo apt install net-tools]
ctcp=$(cat /proc/net/sockstat{,6} | awk '$1 == "TCP:" {print $3}')
ulog=$(users | wc -w)
ip=$(hostname -I)
mac=$(ip link show | awk '$1 == "link/ether" {print $2}')
cmds=$(journalctl _COMM=sudo | grep COMMAND | wc -l) # journalctl should be running as sudo but our script is running as root so we don't need in sudo here
wall "	#Architecture: $arc
	#CPU physical: $pcpu
	#vCPU: $vcpu
	#Memory Usage: $uram/${fram}MB ($pram%)
	#Disk Usage: $udisk/${fdisk}Gb ($pdisk%)
	#CPU load: $cpul
	#Last boot: $lb
	#LVM use: $lvmu
	#Connexions TCP: $ctcp ESTABLISHED
	#User log: $ulog
	#Network: IP $ip ($mac)
	#Sudo: $cmds cmd" # broadcast our system information on all terminals
```

### How does the script works ?

1. The first line of the script indicates that the script is to be executed by the Bash shell.
2. Next, the script defines a series of variables that will be used to store system information. Each variable is initialized with the value returned by an external command call. For example, the pcpu variable contains the number of physical processors on the system, obtained using the grep and uniq commands.
3. Then, the script uses the wall command to display system information on all terminals connected to the system. The information is displayed as preformatted text lines, with each variable inserted at the appropriate place in the string.

Here is a more detailed description of each variable and the external command used to define it:

* **arc**: contains the system architecture, obtained using the **`uname`** command with the **`a`** option which displays all available information about the system.
* **pcpu**: contains the number of physical processors on the system, obtained using the **`grep`** command to find all lines in the **`/proc/cpuinfo`** file that contain the string "physical id", then using **`sort`** and **`uniq`** to remove duplicates and finally **wc** to count the remaining lines.
* **vcpu**: contains the number of virtual processors (or "cores") on the system, obtained using the **`grep`** command to find all lines in the **`/proc/cpuinfo`** file that begin with "processor", then using **`wc`** to count the remaining lines.
* **fram**: contains the total amount of physical memory (in MB) on the system, obtained using the **`free`** command with the **m** option to display memory in MB, then **`awk`** to extract the second column from the line that begins with "Mem:".
* **uram**: contains the amount of used physical memory (in MB) on the system, obtained using the **`free`** command with the **m** option to display memory in MB, then **`awk`** to extract the third column from the line that begins with "Mem:".
* **pram**: contains the percentage of used physical memory on the system, obtained using the **`free`** command without options, then **`awk`** to extract the third column (corresponding to used memory) and divide it by the second column (corresponding to total memory) and multiply the result by 100. The **`printf`** command is used to format the result with two decimal places.
* **fdisk**: contains the total size of the disk (in GB) on the system, obtained using the **`df`** command with the **`Bg`** option to display size in GB and **`grep`** to keep only the lines that begin with "/dev/", except those that end with "/boot$" (this excludes the boot partition from the calculation). **`awk`** is used to add up the sizes of all the partitions and display the result.
* **udisk**: contains the amount of used disk space (in MB) on the system, obtained similarly to **`fdisk`**, but using the **`df`** command with the **`Bm`** option to display size in MB and using the third column (corresponding to used space) instead of the second.
* **pdisk**: contains the percentage of used disk space on the system, obtained similarly to **`pram`**, but using the **`df`** command with the **`Bm`** option to display size in MB and using the third column (corresponding to used space) and the second column (corresponding to total size) instead of physical memory. The **`printf`** command is used to format the result with one decimal place.
* **cpul**: contains the CPU usage percentage of the computer, obtained using the **`top`** command and retrieving the value associated with the line starting with "%Cpu".
* **lb**: contains the date and time of the last boot of the computer, obtained using the **`who -b`** command and retrieving the value associated with the 3rd and 4th columns of the result. The **`who -b`** command displays information about system starts and stops, such as the date and time of the last boot and the last stop.
* **lvmt**: contains the number of storage devices using LVM (Logical Volume Manager) on the computer, obtained using the **`lsblk`** command and counting the number of lines containing the string "lvm".
* **ctcp**: contains the number of TCP connections currently being established on the computer, obtained using the **`/proc/net/sockstat`** and **`/proc/net/sockstat6`** files and retrieving the value associated with the line starting with "TCP:".
* **ulog**: contains the number of users logged in to the computer, obtained using the **`users`** command and counting the number of words (i.e., number of users) in the result.
* **ip**: contains the IP address of the computer, obtained using the **`hostname -I`** command.
* **mac**: contains the MAC address of the computer's network interface, obtained using the **`ip link show`** command and retrieving the value associated with the line starting with "link/ether".
* **cmds**: contains the number of commands executed with sudo on the computer, obtained using the **`journalctl`** command and counting the number of lines containing the string "COMMAND". The **`journalctl`** command displays entries from the system journal, which are events recorded by the operating system. By specifying the filter **`_COMM=sudo`**, only journal entries related to commands executed with **`sudo`** are selected. By counting the number of lines containing the string "COMMAND", the number of commands executed with **`sudo`** is obtained.
* **wall**: sends the message contained in quotation marks to all users logged in to the computer, using the **`wall`** command. The message contains several information about the system, such as the architecture, memory and disk usage, CPU load, date of last boot, IP and MAC address of the network interface, etc. This information is obtained using the variables described above.

### What is cron?

Cron is a daemon (a background process) that runs commands or scripts at predefined intervals of time, called "cron times". It is primarily used on Unix and Linux systems to schedule tasks to be run automatically.

Cron uses a configuration file called "crontab" that defines the tasks to be run and their frequency of execution. Each line in the crontab corresponds to a task to be run, and contains five fields that define when the task should be run.

Here is an example of a crontab that runs a command every day at midnight:

```bash
0 0 * * * /path/to/script
```

Each field in the crontab can be defined in different ways:

* An integer represents an absolute value (for example, to run a task every day at midnight, you would set the first field to 0).
* An asterisk (*) means that the task should be run at all possible values for that field (for example, to run a task every hour, you would set the second field to *).
* A list of values separated by commas (e.g. 1,2,3) means that the task should only be run when the field matches one of these values (for example, to run a task every day of the week except Saturday and Sunday, you would set the fifth field to 1-5).
* A range of values separated by a dash (e.g. 2-5) means that the task should be run when the field matches a value within that range (for example, to run a task every day of the week from Tuesday to Friday, you would set the fifth field to 2-5).

You can use the **`crontab -e`** command to edit your crontab and add or modify tasks to be run. You can also use the **`crontab -l`** command to view the contents of your crontab.

## Bonus

### WordPress site

### FTP service

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

# My B2BR project evaluation

<div align="center">

|      Passed ?      |   Note  |
|--------------------|:-------:|
| ✅                 | 125/100 |

</div>

<div align="center" style="text-align:center">
	<img src="https://raw.githubusercontent.com/rphlr/rphlr/main/imgs/separator.gif" alt="Separator" width ="200">
</div>

This module was done by [rphlr](https://rphlr.ch).
