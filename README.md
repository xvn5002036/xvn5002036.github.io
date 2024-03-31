
在本教程中，我們將使用它 **`Chocolatey Package Manager`** 來幫助我們安裝所有需要的元件，而無需使用瀏覽器點擊此處，點擊那裡，解壓縮這個，解壓縮那個。我們將使用一些簡單的命令，好嗎？

您可以按照 [this video on Youtube](https://youtu.be/BWjmgn07VgE).進行操作。

### 安裝 Chocolatey

開啟具有管理員權限的powershell視窗並執行此命令；

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

#### 停用每次安裝的確認
```css
choco feature enable -n allowGlobalConfirmation
```

#### 安裝軟體包
```css
choco install git mariadb visualstudio2022community notepadplusplus
```


## 安裝 Visual Studio

打開 `Visual Studio Installer`

選擇使用 C++ 及其以下元件進行桌面開發：

- MSVC v143 - VS 2022 C++ x64/x86
- Just-in-Time-debugger
- C++ tools for Windows
- IntelliCode
- C++ AddressSanitizer
- Windows SDK
- vcpkg package manager

如果需要，您也可以選擇進行最小設置。 **但不建議這樣做**.

最小設定 :

- MSVC v143 - VS 2022 C++ x64/x86
- Windows SDK

## 克隆 rAthena 儲存庫

我們只會克隆主分支，這將節省空間和下載時間

We will only clone the master branch, that will save us space and download time

```sql
git clone https://github.com/PandasWS/Pandas.git -b master
```

## 建立資料庫和用戶

我們造訪mariadb控制台
```sh
mysql -u root
```

我們建立資料庫 `rathenadb`

```sql
DROP DATABASE IF EXISTS rathenadb;
CREATE DATABASE IF NOT EXISTS rathenadb DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```
我們建立資料庫 `rathenalog`

```sql
DROP DATABASE IF EXISTS rathenalog;
CREATE DATABASE IF NOT EXISTS rathenalog DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```

我們建立使用者並授予資料庫權限 `rathenadb` and `rathenalog`

!!! 以下記得將`IDENTIFIED BY 'froggopass'`更改 `froggopass `為您想要的任何內容(為數據庫密碼)


```sql
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE ON rathenadb.*TO 'rathenadbusr'@'localhost' IDENTIFIED BY 'froggopass';
FLUSH PRIVILEGES;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE ON rathenalog.* TO 'rathenadbusr'@'localhost';
FLUSH PRIVILEGES;
```

我們退出MariaDB控制台
```cmd
exit
```

創建資料庫後，我們可以用表填充它；;

```powershell
cd Pandas/sql-files
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

### 新增 S1、P1 和新的管理員帳戶

我們 `MariaDB` 再次造訪控制台
```css
mysql -u root
```

我們選擇 `rathenadb` 資料庫
```css
use rathenadb
```
我們新增用戶 `S1` 和密碼 `P1`   `froggos1`為S1`froggop1`為P1 可更改

```sql
UPDATE login set `userid` = "froggos1", `user_pass` = "froggop1" where `account_id` = 1;
```

建立一個 GM Lvl 99 帳戶。 *（可選）*.
```sql
INSERT INTO `login` VALUES (2000000, 'test', 'test', 'M', 'a@a.com', 99, 0, 0, 0, 0, NULL, '', NULL, 0, '', 0, 0, 0, NULL, 0);
```

退出 MariaDB 控制台
```cmd
exit
```
## 進入Pandas資料夾

在 `conf\import\inter_conf.txt`貼上以下代碼 *這裡為連接數據的設定*

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


在 `conf\import\map_conf.txt` 為設定S1及P1

```ruby
userid: froggos1
passwd: froggop1
```

在 `conf\import\char_conf.txt` 為設定S1及P1

pincode_enabled: no  是設定是否要開防外掛按鈕密碼  如果要開啟則設定`pincode_enabled: yes`

```ruby
userid: froggos1
passwd: froggop1

pincode_enabled: no
```



在 `src/custom/defines_pre.hpp`
我們需要在模擬器中聲明packetver，而packetver是基於您選擇的RO客戶端的，在本教程中，我們使用 `2022-04-06` 客戶端進行連接，所以這就是我們聲明的內容，記住格式 `(YYYYMMDD)`

```cpp
#define PACKETVER 20220406
```

!!! 警告 "修改原始碼後記得編譯並重新啟動伺服器"
