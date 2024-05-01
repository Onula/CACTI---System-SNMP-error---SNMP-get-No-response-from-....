## CACTI - System SNMP error - SNMP::get(): No response from ....
This error occurs in CACTI when adding a device or when devices cannot currently connect via Simple Network Management Protocol (SNMP), and is caused by not making the correct SNMP installation and service settings. It also causes Data Query and Graph problems like " ERROR:C:/Apache24/htdocs/cacti/rra/.........rrd" can not exist"




## Installation

### Using Windows Settings

1. Go to **Settings** > **System** > **Optional features**.
2. Click **View features**.
3. Select and install **"SNMP"** and optionally **"WMI SNMP Provider"**.

### Using PowerShell

Alternatively, you can install these features via PowerShell:

1. Open PowerShell as an administrator.
2. Execute the following commands:

    ```powershell
    Add-WindowsCapability -Online -Name "SNMP.Client~~~~0.0.1.0"
    Add-WindowsCapability -Online -Name "WMI-SNMP-Provider.Client~~~~0.0.1.0"
    ```

## Configuration

### Enable and Configure SNMP Service

1. Press `Windows key + R`, type `services.msc`, and press Enter.
2. Find the **"SNMP Service"** in the list, right-click on it, and choose **Properties**.
3. Configure the service:
    - **General tab**: Set the Startup type to **Automatic**.
    - **Agent tab**: Select all services.
    - **Security tab**:
        - Add a community with the name `public` and set rights to **READ ONLY**.
        - Under **"Accept SNMP packets from these hosts"**, add the IP addresses of your monitoring servers (like Cacti, Zabbix, Nagios, etc.). For local setups using XAMPP, you can use `localhost` or your local IP address.
4. Click **Apply** to save the changes.

