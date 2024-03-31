
In this tutorial we are going to use **`Chocolatey Package Manager`** to help us install all the needed components witout using the browser to click here, click there, unzip this, unzip that. We are going to use some plain commands, *all righty* ?

You can follow the tutorial with [this video on Youtube](https://youtu.be/BWjmgn07VgE).

### Install Chocolatey

Open a powershell window with admin rights and execute this command;

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

#### Disable confirmation for each installation
```css
choco feature enable -n allowGlobalConfirmation
```

#### Installing Packages
```css
choco install git mariadb visualstudio2022community notepadplusplus
```


## Install Visual Studio

Open `Visual Studio Installer`

Select Desktop Development with C++ and its following components:

- MSVC v143 - VS 2022 C++ x64/x86
- Just-in-Time-debugger
- C++ tools for Windows
- IntelliCode
- C++ AddressSanitizer
- Windows SDK
- vcpkg package manager

You can also choose to do the minimal setup if you want, although this is **not recommended**.

Minimal Setup:

- MSVC v143 - VS 2022 C++ x64/x86
- Windows SDK

## Clone rAthena Repository

We will only clone the master branch, that will save us space and download time

```sql
git clone https://github.com/rathena/rathena.git -b master
```

## Create Databases and user

We access the mariadb console
```sh
mysql -u root
```

We create the database `rathenadb`

```sql
DROP DATABASE IF EXISTS rathenadb;
CREATE DATABASE IF NOT EXISTS rathenadb DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```
We create the database `rathenalog`

```sql
DROP DATABASE IF EXISTS rathenalog;
CREATE DATABASE IF NOT EXISTS rathenalog DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```

We create users and grant permissions on the databases `rathenadb` and `rathenalog`

!!! warning "Remember to change the `froggopass` to anything you want"


```sql
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE ON rathenadb.*TO 'rathenadbusr'@'localhost' IDENTIFIED BY 'froggopass';
FLUSH PRIVILEGES;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE ON rathenalog.* TO 'rathenadbusr'@'localhost';
FLUSH PRIVILEGES;
```

We exit the MariaDB console
```cmd
exit
```

Once the database is created, we can populate it with tables;

```powershell
cd rathena/sql-files
Get-Content main.sql | mysql -u root rathenadb
Get-Content web.sql | mysql -u root rathenadb
Get-Content logs.sql | mysql -u root rathenalog
Get-Content roulette_default_data.sql | mysql -u root rathenadb
Get-Content item_db.sql | mysql -u root rathenadb
Get-Content item_db2.sql | mysql -u root rathenadb
Get-Content item_db_re.sql | mysql -u root rathenadb
Get-Content item_db2_re.sql | mysql -u root rathenadb
Get-Content item_db_equip.sql | mysql -u root rathenadb
Get-Content item_db_etc.sql | mysql -u root rathenadb
Get-Content item_db_usable.sql | mysql -u root rathenadb
Get-Content item_db_re_equip.sql | mysql -u root rathenadb
Get-Content item_db_re_etc.sql | mysql -u root rathenadb
Get-Content item_db_re_usable.sql | mysql -u root rathenadb
Get-Content mob_db.sql | mysql -u root rathenadb
Get-Content mob_db2.sql | mysql -u root rathenadb
Get-Content mob_db_re.sql | mysql -u root rathenadb
Get-Content mob_db2_re.sql | mysql -u root rathenadb
Get-Content mob_skill_db.sql | mysql -u root rathenadb
Get-Content mob_skill_db2.sql | mysql -u root rathenadb
Get-Content mob_skill_db_re.sql | mysql -u root rathenadb
Get-Content mob_skill_db2_re.sql | mysql -u root rathenadb
```

### Add S1, P1 and a new admin account 

We access the `MariaDB` console again
```css
mysql -u root
```

We select the `rathenadb` database
```css
use rathenadb
```
We add the user `S1` and the password `P1`

```sql
UPDATE login set `userid` = "froggos1", `user_pass` = "froggop1" where `account_id` = 1;
```

Create a GM Lvl 99 account *(Optional)*.
```sql
INSERT INTO `login` VALUES (2000000, 'test', 'test', 'M', 'a@a.com', 99, 0, 0, 0, 0, NULL, '', NULL, 0, '', 0, 0, 0, NULL, 0);
```

Exit the MariaDB console
```cmd
exit
```
## Conf Folder

In `import\inter_conf.txt`

```ruby
login_server_id: rathenadbusr
login_server_pw: froggopass
login_server_db: rathenadb

ipban_db_id: rathenadbusr
ipban_db_pw: froggopass
ipban_db_db: rathenadb

char_server_id: rathenadbusr
char_server_pw: froggopass
char_server_db: rathenadb

map_server_id: rathenadbusr
map_server_pw: froggopass
map_server_db: rathenadb

web_server_id: rathenadbusr
web_server_pw: froggopass
web_server_db: rathenadb

log_db_id: rathenadbusr
log_db_pw: froggopass
log_db_db: rathenalog
```


In `import\map_conf.txt`

```ruby
userid: froggos1
passwd: froggop1
```

In `import\char_conf.txt`

```ruby
userid: froggos1
passwd: froggop1

pincode_enabled: no
```



In `src/custom/defines_pre.hpp`
We need to declare the packetver in our emulator, and the packetver is based on the RO client of your choosing, in this tutorial, we are using a `2022-04-06` client to connect, so that's what we declare, remember the format `(YYYYMMDD)`

```cpp
#define PACKETVER 20220406
```

!!! warning "Remember to compile and restart server after changing the source code"
