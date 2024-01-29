#### Search for `turn windows features on or off` in your system
![[23.12.2023_22.44.32_REC.png]]
#### Select the check box for `windows linux subsytem
![[23.12.2023_22.45.29_REC.png]]
### Install WSL :
```bash
#open windows conmmand and run as administrator 
#then enter the below command. 
wsl --install
```



![[WhatsApp Image 2023-12-21 at 9.56.09 AM.jpeg]]	
### Install Ubuntu 22.04.3
![[WhatsApp Image 2023-12-21 at 9.56.08 AM.jpeg]]

![[21.12.2023_12.25.32_REC.png]]

![[WhatsApp Image 2023-12-21 at 9.56.08 AM (2).jpeg]]

```bash

#open ubuntu 22.4.3 LTS and run this linux commands one by one.

sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt-get install git
sudo apt-get install python3-dev python3.10-dev python3-setuptools python3-pip python3-distutils
sudo apt-get install python3.10-venv
sudo apt-get install software-properties-common
sudo apt install mariadb-server mariadb-client
sudo apt-get install redis-server
sudo apt-get install xvfb libfontconfig wkhtmltopdf
sudo apt-get install libmysqlclient-dev
sudo service mariadb start
```

### Setup root password by following this images:
```shell
sudo mysql_secure_installation
```
![[WhatsApp Image 2023-12-24 at 1.06.45 AM.jpeg]]
![[WhatsApp Image 2023-12-24 at 1.06.45 AM (1).jpeg]]
![[WhatsApp Image 2023-12-24 at 1.06.45 AM (2).jpeg]]
### Then do the following
```shell
sudo nano /etc/mysql/my.cnf
```
Add the below code block at the bottom of the file:
```service
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
[mysql]
default-character-set = utf8mb4
```

![[WhatsApp Image 2023-12-21 at 9.56.08 AM (1).jpeg]]
##### After pasting the code block. Ctrl+x , press y and press enter to exit.

```shell
#Then again continue with this below linux commands one by one. 
sudo service mariadb restart
sudo apt install curl
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
#if this doesnt work means try this below code or else go to the official web site check the command for latest update.
#curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

source ~/.profile
nvm install v16.15.0
sudo apt-get install npm
sudo npm install -g yarn
sudo pip3 install frappe-bench
bench init frappe-bench --frappe-branch version-14 --frappe-path https://github.com/frappe/frappe.git
cd frappe-bench
bench new-site site1.local
bench get-app https://github.com/frappe/erpnext.git --branch version-14
bench --site site1.local install-app erpnext
cd sites
ls
nano currentsite.txt
#Enter the name of the site in local
#site1.local
```

### Enable developer mode:
![[activating dev mode in frappe.png]]
```shell
#do the following steps one by one
cd frappe-bench
cd sites
ls
cd site1.local
ls
nano site_config.json
```
_copy __"developer_mode":1__ followed by comma(,) after "mariadb",_
	![[dev mode.png]]
	


# Installation in VS Code :
#### ___Install VS code___ :
![[WhatsApp Image 2023-12-21 at 9.56.07 AM.jpeg]]
1. Open the VS code application
2. Go to the extension tab and install WSL! ![[1.jpeg]]
3. Click on down left corner.
![[2 1.jpeg]]
4. Select connect to WSL using Distro.
![[WhatsApp Image 2023-12-24 at 12.45.04 PM.jpeg]]
5. Select Ubuntu-22.04.![[WhatsApp Image 2023-12-24 at 12.45.06 PM (7).jpeg]]
6. Go to debugger tab and click on create a launch json ![[3 1.jpeg]]
7. Select frappe-bench and click ok.![[4.jpeg]]
8. Tick the check box and  click yes, I trust the authors![[572039c3-5b19-4f1c-8cd3-0f62c6c574ec.jpg]]
9. Our aim is to get this Bench and launch chrome option in debug tab of vs code. If got it means the process is now completed or else try the below method.
 ![[7 1.jpeg]]
 
1. Frappe Bench will be opened. After bench opens, In _.vscode_ if there is any json file remove it.
![[WhatsApp Image 2023-12-24 at 12.45.07 PM.jpeg]]
2. create a ___launch.json___ file under ___.vscode___
![[WhatsApp Image 2023-12-24 at 12.45.05 PM.jpeg]]
3. In the empty launch.json you created, copy the full below code and paste it.
```json
{

    // Use IntelliSense to learn about possible attributes.

    // Hover to view descriptions of existing attributes.

    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387

    "version": "0.2.0",

    "configurations": [

    { "type": "pwa-chrome",

    "request": "launch",

    "name": "Launch Chrome",

    "url": "http://localhost:8000",

    "webRoot": "${workspaceFolder}"

    // "runtimeArgs": ["--incognito"]

    },

    {

    "name": "Bench",

    "type": "python",

    "request": "launch",

    "program": "${workspaceFolder}/apps/frappe/frappe/utils/bench_helper.py",

    "args": [

    "frappe",

    "serve",

    "--port",

    "8000",

    "--noreload",

    "--nothreading"

    ],

    "python": "${workspaceFolder}/env/bin/python",

    "cwd": "${workspaceFolder}/sites",

    "env": {

    "DEV_SERVER": "1"

    },

    "justMyCode": false

    }

    ]

}
```
 ![[WhatsApp Image 2023-12-24 at 12.45.06 PM (5).jpeg]]
 Save the file by ctrl+s 
 ![[5.jpeg]]
 Finally navigate to Debug tab you can see the bench and launch chrome option
 start them one by one Respectively. 
 ![[6.jpeg]]

Click here for [[Frappe App Creation]]