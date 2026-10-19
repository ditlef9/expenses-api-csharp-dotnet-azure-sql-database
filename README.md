# expenses-api-csharp-dotnet-azure-sql-database
An organization has an application that manages employee expense claims. The API stores the claims in Azure SQL Database, while Microsoft Entra ID handles user identities and authentication.

🕸️ Norsec1 Website (PHP) - norsec1.com
<!-- Keywords: Norsec1, Website, PHP, cybersecurity, trust, innovation. Light version. -->
<!-- Style preference: Modern. Color palette: You select. Symbols or motifs: Norway. Typography: Monospaced. Logo shape: You select. -->

Welcome to the Norsec1 website repository. Norsec1 is a cybersecurity company based in Norway, specializing exclusively in **vulnerability management**. 

This PHP-based website serves as the company’s online presence, combining local expertise and global best practices to highlight our focus on identifying and mitigating security weaknesses. This repo contains all source code and deployment instructions for running the site locally and in production.



---

## Table of Contents


1. [🔗 Useful Links](#-1-useful-links)<br>
2. [🖌️ System Architecture Diagram for Norsec1 Website (PHP)](#%EF%B8%8F-2-system-architecture-diagram-for-norsec1-website-php)<br>
3. [🌍 Business Idea](#-3-business-idea)<br>
4. [🚀 Deploy to Production from Windows](#-4-deploy-to-production-from-windows)<br>
5. [🖋️ Create New PHP Pages](#%EF%B8%8F-4-create-new-php-pages)<br>
6. [⚙️ Run locally with Apache with PHP and MariaDB on Windows](#%EF%B8%8F-6-run-locally-with-apache-with-php-and-mariadb-on-windows)<br>
7. [🐳 Run locally with Docker on Mac](#%EF%B8%8F-6-run-locally-with-docker-on-mac)<br>
8. [✨ Linting and Security](#-6-linting-and-security)<br>
9. [📋 Application Details and Environment Overview for Norsec1 Website (PHP)](#-7-application-details-and-environment-overview-for-norsec1-website-php)<br>
10. [📜 License](#-8-license)<br>

---



## 🔗 1 Useful Links

- 🌐 **[Company Website – norsec1.com](https://norsec1.com)**  
  Research, testing, and staying ahead of cybersecurity threats.

- ☁️ **[Web Hosting – one.com](https://one.com)**

- 💻 **GitHub Repositories**
  - 🕸️ [Norsec1 Website (PHP)](https://github.com/ditlef9/website-norsec1-php) – Company site source code (You are here!)
  - 🛠️ [Vulnerability Manager Webapp (PHP)](https://github.com/ditlef9/webapp-vulnerability-management-php) – Webapp Vulnerability Manager
  - 🐍 [Vulnerability Agent (Python)](https://github.com/ditlef9/agent-vulnerability-management-norsec1) – Cross-platform scanning agent (Windows, Ubuntu, Mac)


---

## 🖋️ 2 System Architecture Diagram for Norsec1 Website (PHP)

* Where Norsec1 Website runs: One.com
* Programming languages: PHP and MySQL
* Dependencies: None. 
* System Architecture Diagram (visual illustration of a system's various components and show how they communicate and interact with each other):

![_docs/system-architecture-diagram-for-norsec1-website.drawio.png](_docs/system-architecture-diagram-for-norsec1-website.drawio.png)

---

## 🌍 3 Business Idea
Norsec1 is a cybersecurity company focused on **vulnerability management** for small and mid-sized organizations in Norway. Our goal is to simplify and modernize how businesses detect, track, and fix software vulnerabilities — without requiring a dedicated security team.

We believe in **transparency, automation, and accessibility**, providing actionable insights

[Business Idea](README-BUSINESS-IDEA.md) – Cross-platform scanning agent (Windows, Ubuntu, Mac)

---

## 🚀 4 Deploy to Production from Windows

**Install WSL**<br>
1. Download WSL by running the following Powershell command as administrator:
```wsl --install```

* Username: user
* Password: Your Windows Password

2. Restart Windows
3. Open Ubuntu and install tools:
```
sudo apt update
sudo apt install -y rsync openssh-client
```

**Connect**<br>
```ssh SFTP_USERNAME@FTP_ADDRESS```

**Directories**<br>
C:\Apache24\htdocs\website-ekeberg-php  >   /webroots/07f76d87<br>
C:\Apache24\htdocs\vm-app-norsec1-php   >   /webroots/b1c42d74<br>

**Upload website**<br>
* Dyrun:<br>
```
cd /mnt/c/Apache24/htdocs/website-ekeberg-php

rsync -av --delete --dry-run \
  --exclude-from=/mnt/c/Apache24/htdocs/website-ekeberg-php/.rsyncignore \
  /mnt/c/Apache24/htdocs/website-ekeberg-php/ \
  USERNAME@FTP_ADDRESS:/webroots/07f76d87/
```

* Deploy:<br>
```
cd /mnt/c/Apache24/htdocs/website-ekeberg-php


rsync -av --delete \
  --exclude-from=/mnt/c/Apache24/htdocs/website-ekeberg-php/.rsyncignore \
  /mnt/c/Apache24/htdocs/website-ekeberg-php/ \
  USERNAME@FTP_ADDRESS:/webroots/07f76d87/
```


**Upload app**<br>
* Dyrun:<br>
```
cd /mnt/c/Apache24/htdocs/webapp-vulnerability-management-php

rsync -av --delete --dry-run \
  --exclude-from=/mnt/c/Apache24/htdocs/webapp-vulnerability-management-php/.rsyncignore \
  /mnt/c/Apache24/htdocs/webapp-vulnerability-management-php/ \
  USERNAME@FTP_ADDRESS:/webroots/b1c42d74/
```

* Deploy:<br>
```
cd /mnt/c/Apache24/htdocs/webapp-vulnerability-management-php


rsync -av --delete \
  --exclude-from=/mnt/c/Apache24/htdocs/webapp-vulnerability-management-php/.rsyncignore \
  /mnt/c/Apache24/htdocs/webapp-vulnerability-management-php/ \
  USERNAME@FTP_ADDRESS:/webroots/b1c42d74/
```

**WinSCP**<br>
Additionally you may want to download WinSCP

Options > Preferences > Transfer
* [v] Background transfer
 
Options > Preferences > Transfer > Drag & Drop
* [v] Download files via temporary folder

Tabs > Sites > Norsec1.com > Edit > Advanced:
* Enviroment > Directories
  * [ ] Synchronize browsing
  * [ ] Remember last used directory
  * Remote directory: /customers/e/f/b/cq6oky39x/webroots/07f76d87
  * Local directory: C:\Apache24\htdocs\website-ekeberg-php
  * [ ] Cache visited remote directories
  * [ ] Cache directory changes
  * [ ] Permanent cache
* Bg color: #D6ECFA RGB: 185, 167, 227

Tabs > Sites > App.Norsec1.com > Edit > Advanced:
* Enviroment > Directories
  * Remote directory: /customers/e/f/b/cq6oky39x/webroots/b1c42d74
  * Local directory: C:\Apache24\htdocs\vm-app-norsec1-php
  * [ ] Cache visited remote directories
  * [ ] Cache directory changes
  * [ ] Permanent cache
* Bg color: #B9A7E3 RGB: 214, 236, 250



---

## 🖋️ 5 Create New PHP Pages

---

## ⚙️ 6 Run locally with Apache with PHP and MariaDB on Windows

### 6.1 Apache

* Install VC_redist.x64.exe from https://aka.ms/vs/17/release/VC_redist.x64.exe (restart not nessesary)
* Download Apache from https://www.apachelounge.com/download/
* Extract zip to c:\Apache24

* Create a file `StartApache.bat` that will start Apache server for you:

```
@echo off
echo Starting Apache HTTP Server...
start "" "C:\Apache24\bin\httpd.exe"
echo Apache started. This window will close in 20 seconds...
timeout /t 20 >nul
exit
```

* You can now go to http://localhost/

### 6.2 PHP
* Download Thread Safe PHP from https://windows.php.net/download/
* Extract ZIP to c:\php
* Rename C:\php\php.ini-development to C:\php\php.ini.
* Enable the following in php.ini:
  
```
extension=curl
extension=fileinfo
extension=gd
extension=mbstring
extension=mysqli
extension=pdo_mysql
extension=sodium
extension=zip
```

Edit the Max file size to 100 MB and the memory limit to 512 MB:
```
upload_max_filesize = 100M
memory_limit = 512M
post_max_size = 100M
```

Edit output buffering:
```
output_buffering = 0
```

* Add C:\php to the PATH environment variable: Start > Settings > System > About > Advanced system settings > Enviroment variables > System variables: Path > [Edit] 

**Configure Apache**
* Stop Apache
* Edit `C:\Apache24\conf\httpd.conf`

Add the following at the bottom:
```
# PHP8 module
PHPIniDir "C:/php"
LoadModule php_module "C:/php/php8apache2_4.dll"
AddType application/x-httpd-php .php
```

* Change the DirectoryIndex setting to use index.php 


```
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>
```


### 6.3 MariaDB

* Download MariaDB for MS Windows 64-bit (mariadb-11.7.2-winx64.msi): https://mariadb.com/downloads/
* Install it to C:\Program Files\MariaDB 11.7\
  * Example password: root
  * TCP Port: 3306
* Open HeidiSQL to create databsae:
  * IP: 127.0.0.1
  * User: root
  * Password: root
  * In Heidi Right Click on Unnamed and select `Create database ...`.
    * Name: `norsec1`
    * Name: `phpmyadmin`.

### 6.4 phpMyAdmin

* Download phpMyAdmin: https://www.phpmyadmin.net/downloads/
* Extract to C:\Apache24\htdocs\phpmyadmin
* Open C:\Apache24\htdocs\phpmyadmin\config.sample.inc.php and rename it to config.inc.php.

Edit it with a text editor and add a blowfish_secret:
```
$cfg['blowfish_secret'] = 'randomSecretKey123!';
```

Remove comments from the *configuration storage settings*:
```
/**
 * phpMyAdmin configuration storage settings.
 */

/* User used to manipulate with storage */
$cfg['Servers'][$i]['controlhost'] = 'localhost';
// $cfg['Servers'][$i]['controlport'] = '';
$cfg['Servers'][$i]['controluser'] = 'pma';
$cfg['Servers'][$i]['controlpass'] = 'pmapass';

/* Storage database and tables */
$cfg['Servers'][$i]['pmadb'] = 'phpmyadmin';
$cfg['Servers'][$i]['bookmarktable'] = 'pma__bookmark';
$cfg['Servers'][$i]['relation'] = 'pma__relation';
$cfg['Servers'][$i]['table_info'] = 'pma__table_info';
$cfg['Servers'][$i]['table_coords'] = 'pma__table_coords';
$cfg['Servers'][$i]['pdf_pages'] = 'pma__pdf_pages';
$cfg['Servers'][$i]['column_info'] = 'pma__column_info';
$cfg['Servers'][$i]['history'] = 'pma__history';
$cfg['Servers'][$i]['table_uiprefs'] = 'pma__table_uiprefs';
$cfg['Servers'][$i]['tracking'] = 'pma__tracking';
$cfg['Servers'][$i]['userconfig'] = 'pma__userconfig';
$cfg['Servers'][$i]['recent'] = 'pma__recent';
$cfg['Servers'][$i]['favorite'] = 'pma__favorite';
$cfg['Servers'][$i]['users'] = 'pma__users';
$cfg['Servers'][$i]['usergroups'] = 'pma__usergroups';
$cfg['Servers'][$i]['navigationhiding'] = 'pma__navigationhiding';
$cfg['Servers'][$i]['savedsearches'] = 'pma__savedsearches';
$cfg['Servers'][$i]['central_columns'] = 'pma__central_columns';
$cfg['Servers'][$i]['designer_settings'] = 'pma__designer_settings';
$cfg['Servers'][$i]['export_templates'] = 'pma__export_templates';
```


* Visit http://localhost/phpmyadmin/
* Username: root
* Password: root

Create a database named `phpmyadmin` using `Heidi`.
  
### 6.5 Checkout Norsec1 Website (PHP)

Checkout:<br>
```
cd c:\Apache24\htdocs
git clone https://github.com/ditlef9/website-norsec1-php.git
```

* Now visit http://localhost/website-norsec1-php


### Debug:

#### Check Apache:

```
cd C:\Apache24\bin
httpd -v
```

Correct output: 
```
Server version: Apache/2.4.65 (Win64)
Apache Lounge VS17 Server built:   Jul 24 2025 14:32:297
```

#### Check PHP:

With CMD run the following (does not mather what directory you are in):

```
php -v
```

Corect output:

```
PHP 8.4.10 (cli) (built: Jul  2 2025 11:04:43) (ZTS Visual C++ 2022 x64)
Copyright (c) The PHP Group
Zend Engine v4.4.10, Copyright (c) Zend Technologies
```


# 6.6 Download CA bundle

**Download curl CA extract**<br>
* Go to curl CA extract: https://curl.se/docs/caextract.html.
* Download `cacert.pem` to `C:\php\extras\ssl\cacert.pem`

**Add to php**
Open C:\php\php.ini and add or modify the following line:

```
[curl]
curl.cainfo = "C:\php\extras\ssl\cacert.pem"
```

# 6.7 Composer

Install compoer from https://getcomposer.org/

# 6.8 ImageMagic

Install ImageMagic:
* Download ImageMagic from https://imagemagick.org/script/download.php#windows > Windows binary release >
  ***-Q16-HDRI-x64-dll.exe
* Restart computer because variable needs to be in the system PATH.

Install PHP extension:
* https://mlocati.github.io/articles/php-windows-imagick.html:
  - Thread safe: Yes
  - Architecture: x64
  - Example file:	php_imagick-3.4.3-5.5-ts-vc11-x64.zip
* Copy php_imagick.dll to C:\php\ext
* Copy rest of dll to c:\php
* Open C:\php\php.ini
* Add this line: `extension=imagick`

Check installation:
* Add a file phpinfo.php: `<?php phpinfo(); ?>`
* Search for imagick

---

## 🐳 7. Run locally with Docker on Mac

Start Colima:

```
colima start --network-address --memory 8 --cpu 2
```

Docker should now be started and this command should list no pods:
```
docker ps
```

Start the application (only website Norsec1 PHP, if you want to start the app and the website head over to the other project):
```
docker compose up --build
```

Visit the application:<br>
http://localhost:8001

phpMyAdmin:<br>
http://localhost:8000

Credentials:
* host = "db";
* user = "myuser";
* pass = "mypassword";
* db   = "norsec1";


Database changes are stored in the db_data Docker volume and will persist when restarting with docker compose up.

Stop the application - Press Control+C or write:
```
docker compose down
```

## 7.2 Debugging Docker Errors:

**Container mysql-db Error response from daemon: Conflict. The container name "/mysql-db" is already in use by co...**<br>

Delete all containers, then restart:

```
docker container prune
docker compose up --build
```

**Error response from daemon: failed to set up container networking: driver failed programming external connectivity on endpoint mysql-db (b975969bd605244d15c7101f9e8141c3649906b43b66e378e159e5c521823f42): Bind for :::3306 failed: port is already allocated**

The app VM-App-Norsec1-PHP has a special docker-compose file. It will lunch:
* website-norsec1-php on port 8001
* webapp-vulnerability-management-php on port 8002
* MySQL on port 3306
* phpMyAdmin on port 8000

This means that if you already have that other app running, then you need to stop that container, 
before starting this container.





---


## ✨ 8. Linting and Security

**Linting job**<br>
Finds all PHP files and runs the built-in PHP linter (php -l) to catch syntax errors early.

**Security job**<br>
Runs only if linting passes successfully. It installs project dependencies and uses the Enlightn Security Checker to scan for known security vulnerabilities in dependencies.

**Snyk**<br>
The project is imported to Snyk also. Log in with GitHub at 
(app.snyk.io)[https://app.snyk.io].

---

## 📋 9. Application Details and Environment Overview for Norsec1 Website (PHP)

* System owner: Sindre Ditlefsen
* Administrator: Sindre Ditlefsen
* Commercial responsibility: Sindre Ditlefsen
* Contributors: 
* Environment: Fullstack
* Business criticality: Critical (Low, Medium, High, Critical)
* Lifecycle: Production (Sandbox, Development, Production)

System Owner:
The system owner is the requirement setter and responsible for the system.
The system owner is responsible for ensuring that the system complies with internal policies, 
that routines are established for the use of the system, that security is adequately maintained, 
and that training in proper use is provided.

System Administrator:
A system administrator carries out the responsibility for the operation of the system on 
behalf of the system owner.

Platform Responsible:
A platform responsible person is accountable for ensuring that the code runs.

Commercial Responsibility:
Responsible for ensuring that payments are made in accordance with guidelines.

---

## 📜 10 License

