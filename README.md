This [EnvoyinStack](https://mirrors.infvie.org/envoyinstack/) script is written using the shell, in order to quickly deploy (Linux, Nginx/OpenResty, MySQL in a production environment/MariaDB/, JAVA,ElasticStack), applicable to Cent
OS 7~ 8(including redhat) of 64.

Script properties:
- Continually updated, Provide Shell Interaction and Autoinstall
- Source compiler installation, most stable source is the latest version, and download from the official site
- Some security optimization
- Providing a plurality of database versions (MySQL-8.0, MySQL-5.7, MySQL-5.6, MariaDB-10.6, MariaDB-10.5, MariaDB-10.4, PostgreSQL, MongoDB)
- Provide Nginx, OpenResty, Rabbitmq, Fastdfs + Fastdht
- Provide Mysql group replication and Proxysql,multi source replication(master slaves)
- Provide Gateway kong server and konga
- Provide Automatically push keys to remote servers
- Providing a plurality of Tomcat version (Tomcat-10,Tomcat-9, Tomcat-8, Tomcat-7)
- Providing a plurality of JDK version (JDK-11.0, JDK-1.8, JDK-1.7)
- Install redis according to their needs
- Jemalloc optimize MySQL, Nginx
- Provide Nginx/OpenResty/Tomcat, MySQL/MariaDB, Redis upgrade script
- Provide local,remote(rsync between servers),Aliyun OSS backup script

## Installation
Install the dependencies for your distro, download the source and run the installation script.

#### CentOS/Redhat

```bash
yum -y install wget screen
```

If you disconnect during installation, you can execute the command `screen -r runname` to reconnect to the install window
```bash
screen -S envoyinstack 
```

If you need to modify the directory (installation, data storage, Nginx logs), modify `options.conf` file before running install.sh
```bash
./install.sh
```
##### Eg :

Automatically push keys to remote servers
```bash
set remote servers list(./tools/iplist.txt) ==> run ./keygen.sh
./install.sh --keygen 

```
Install Nginx
```bash
./install.sh --nginx_option 1 
```
Install OpenResty
```bash
./install.sh --nginx_option 2
```
Install Tomcat
```bash
./install.sh --tomcat_option 1 
```
Install Java
```bash
./install.sh --jdk_option 1 
```
Install MySQL/MariaDB/PostgreSQL/MongoDB
```bash
./install.sh --db_option 1 --dbinstallmethod 1 --dbrootpwd Infvie123456
```
Install Redis
```bash
./install.sh --redis
```
Install Rabbitmq
```bash
./install.sh --rabbitmq
```
Install Fastdfs + Fastdht
```bash
./install.sh --fastdfs
```
Install Mysql group replication and Proxysql
```bash
set vars config
~/envoyinstack/include/replmgr/deploy/ansible/mysql/vars/{group_replication.yaml,master_slaves.yaml,multi_source_replication.yaml}
set template config
~/envoyinstack/include/replmgr/deploy/ansible/mysql/template/
set run config
~/envoyinstack/include/replmgr/config.yaml

./install.sh --replmgr
```
Install Mysql master slaves
```bash
./install.sh --replms
```
Install Mysql multi source replication
```bash
set run config
mtls_with_mysql_group_replication: 0

./install.sh --replmsr
```
Install Gateway kong server and konga
```bash
./install.sh --kong
```
## How to backup

```bash
~/envoyinstack/backup_setup.sh    // Backup parameters
~/envoyinstack/backup.sh    // Perform the backup immediately
crontab -l    // Can be added to scheduled tasks, such as automatic backups every day 1:00
0 1 * * * cd ~/envoyinstack/backup.sh  > /dev/null 2>&1 &
```

## How to upgrade

```bash
~/envoyinstack/upgrade.sh
```

## How to uninstall

```bash
~/envoyinstack/uninstall.sh
```

## Installation

For feedback, questions, and to follow the progress of the project: <br />
Tencent QQ : 1473934158 <br />
[Telegram Group](https://t.me/ErinYeo)<br />
[Infvie Envoy. All Rights Reserved.](https://www.infvie.com)<br />
