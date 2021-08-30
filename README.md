Environmental requirements
After testing and modifying the installation script, danted currently supports the following system versions:

System type	Version
Centos 6 series	6.0
---	6.2
---	6.3
---	6.4 (recommended)
---	6.5
---	6.6
---	6.7
---	6.8
Centos 7 series	7.1
---	7.2
ubuntu series	12.04
---	14.04.2
---	14.04.3
---	14.04.5
---	15.10
---	16.04
Oracle linux series	6.5
---	7.1
---	7.2
Installation options
It is recommended to use the rpm package for installation: rpm -ivh dante-1.4.1-5.x86_64.rpm

Options	describe
--port=socks5	Port number
--ip=;;	Configured IP address, all enabled by default, use; divided
--user=	pam authentication username
--passwd=	Pam authentication user password
--master=	Authentication-free address, such as github.com or 8.8.8.8/32
Use case:
wget --no-check-certificate https://github.com/trungkien006/danted.sock5/raw/main/danted_install.1.4.3.sh -O danted_install.sh 
bash danted_install.sh

bash danted_install.sh --port="1000" --ip="192.168.199.206" --user="zk" --passwd="123456"

Features
1. Use dante stable version 1.4.3 to compile and install.
2. Automatically identify the system IP (default excluded 192.168.0. , 10.0.0. , 127.0.0.*), according to the installation command to select part of the IP or all IP installation (multi-IP environment).
3. Using PAM user authentication, authentication does not need to add system users (the process user sock is added by default), and it is convenient and safe to delete and add users.
4. View the running status of sock5, and it will load automatically after the system starts.
5. Perfect support for multi-access import and export (multi-IP environment, support the use of IP-1, access to the website IP query is IP-1).
6. Optional authentication methods: no username and password, system username and password, Pam username and password
7. Perfect support for Centos/Ubuntu/Debian, automatically identify the system for installation and configuration. [Note that after feedback, Centos 5 cannot be used. ]
8. Customize the authentication method for the connecting client, support the whitelist, that is, support certain IP/IP segments to connect without authentication.
installation steps
1. Download the danted_install.sh script
2. [Optional] Modify the default parameters, DEFAULT_PORT is the default port, DEFAULT_USER PAM user name, DEFAULT_PAWD PAM user corresponding password MASTER_IP is the authentication-free whitelist (domain name, IP optional: such as default buyvm.info or specific IP 8.8.8.8 /32)
3. After modification, execute bash danted_install.sh (refers to using default parameters)
4. If Dante Server Install Successfuly is displayed after the operation is over, it means success. If Dante Server Install Failed! is displayed, the installation failed.
Note: You can also know the configuration parameters dynamically, execute the command as follows:

bash danted_install.sh --port="1000" --ip="192.168.199.206" --user="zk" --passwd="123456"

Instructions for use after installation
1. Command parameters /etc/init.d/danted {start|stop|restart|status|add|del}
2. Restart sock5 /etc/init.d/danted restart or service danted restart
3. Close sock5 /etc/init.d/danted stop or service danted stop
4. Open sock5 /etc/init.d/danted start or service danted start
5. View sock5 status /etc/init.d/danted status or service danted status
6. Add SOCK5 PAM user/change password /etc/init.d/danted add username and password
7. Delete SOCK5 PAM user /etc/init.d/danted del username
8. Configuration file path /etc/danted/sockd.conf
9. Logging path /var/log/danted.log
10.danted help command danted --help
Precautions for use
1. Most browsers (except Opera) do not support Socks5 with password authentication, so you need to install software such as proxifier/proxycap for verification.

2. If it is a fixed IP/Ip segment, you can modify the configuration file and set up whitelist access.

  a.Go to /etc/danted/ to find the configuration file

  b.Modify the from: Master_IP/32 to: 0.0.0.0/0 under the first pass {} module. Modify Master_IP/32 to the IP segment/IP address that needs to use a proxy, such as 114.114.114.0/24 or 5.5.5.5 /32. Multiple access sources, please copy multiple client pass {} modules
  
  c.Restart Danted: service danted restart
3. To delete danted, please refer to the following command to delete the program file

  service danted stop

  rm -rf /etc/danted/

  rm -f /etc/init.d/danted
Remaining problem
Analyze log to count the users connected to sock5.
