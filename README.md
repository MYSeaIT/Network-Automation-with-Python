# Network-Automation-with-Python

These are my projects which I have tested in a real network of 2500+ devices. Scripts created to automate tasks in network devices such as Cisco, HP, Arista, etc.

## Development Process

The process of automation involved creating Python scripts to interface with network devices over SSH using `netmiko` and `paramiko`. Credentials are securely handled, and `datetime` is used for timestamping backups.

The backup scripts for HP and Cisco devices are run from the command line, and the scripts generate backups of the device configurations.

### Encountered Errors and Resolutions

### HP Backup Script (`HP_Backup.py`)

Error: NetMikoTimeoutException  
Cause: Could not establish an SSH connection to the device (possibly due to incorrect IP or device being unreachable).  
Resolution: Ensured IP addresses were up to date and reachable; implemented error handling to log unreachable devices without halting the automation process.

Error: NetMikoAuthenticationException  
Cause: Incorrect username/password authentication for devices.  
Resolution: Added a password confirmation step in `get_credentials()` to avoid mistyped passwords.

Error: SSHException and IOError  
Cause: General SSH errors and IO-related errors (such as writing to a file).  
Resolution: Implemented broader exception handling to catch these errors and log them appropriately.

Error: Incorrect Command Usage  
Cause: Using commands that were not recognized by the device's command-line interface.  
Resolution: Reviewed and updated command syntax to match the device-specific command line.

### Cisco Devices Backup Script (`Cisco_Devices_Backup.py`)

Error: NetMikoTimeoutException  
Cause: Device did not respond in time for an SSH connection.  
Resolution: Configured a retry mechanism with a delay and verified network connectivity.

Error: NetMikoAuthenticationException  
Cause: Authentication failures due to incorrect credentials.  
Resolution: Re-verification of credentials and error-handling logic to prompt the user again for credentials upon failure.

Error: Handling Special Characters in Prompts  
Cause: Device prompts containing special characters leading to execution issues.  
Resolution: Utilized `expect_string` parameter to handle special characters in prompts accurately.
