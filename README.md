## CACTI - System SNMP error - SNMP::get(): No response from ....
This error occurs in CACTI when adding a device or when devices cannot currently connect via Simple Network Management Protocol (SNMP), and is caused by not making the correct SNMP installation and service settings. It also causes Data Query and Graph problems like " ERROR:C:/Apache24/htdocs/cacti/rra/.........rrd" can not exist"

____________________________________________________________________________________________________

#FOR WINDOWS

1. Installing SNMP Service and WMI SNMP Provider

Via Settings: Go to Settings > System > Optional features > View features. Select and install "SNMP" and, optionally, "WMI SNMP Provider".
Via PowerShell: Open PowerShell as an administrator and input the following commands:
```powershell
Add-WindowsCapability -Online -Name "SNMP.Client~~~~0.0.1.0"
Add-WindowsCapability -Online -Name "WMI-SNMP-Provider.Client~~~~0.0.1.0"
```
2.Enable and Configure SNMP Service

1. Press `Windows key + R`, type `services.msc`, and press Enter.
2. Find the **"SNMP Service"** in the list, right-click on it, and choose **Properties**.
3. Configure the service:
    - **General tab**: Set the Startup type to **Automatic**.
    - **Agent tab**: Select all services.
    - **Security tab**:
        - Add a community with the name `public` and set rights to **READ ONLY**.
        - Under **"Accept SNMP packets from these hosts"**, add the IP addresses of your monitoring servers (like Cacti, Zabbix, Nagios, etc.). For local setups using XAMPP, you can use `localhost` or your local IP address.
4. Click **Apply** to save the changes.
___________________________________________________________________________________________________________

FOR LINUX :

1.install SNMP (When prompted, type “Y” to continue)
```bash 
sudo apt install snmpd snmp libsnmp-dev
```
2.Make a backup of the original snmpd.conf file:
```bash 
sudo cp /etc/snmp/snmpd.conf /etc/snmp/snmpd.conf.bak
```
3. Edit the snmpd.conf file:
```bash
sudo nano /etc/snmp/snmpd.conf
```
4.Locate and change the agentAddress to:
```bash
agentAddress udp:161
```
5.Find and add in rocommunity's the following line:
```bash 
rocommunity public
```
6. Save & exit the file
7.Reload the snmpd service:
```bash
sudo service snmpd restart
```
