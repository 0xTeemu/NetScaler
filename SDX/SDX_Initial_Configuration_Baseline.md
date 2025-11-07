# Intial configurations to new SDX

## Description
Reference: https://docs.netscaler.com/en-us/netscaler-adc-secure-deployment

NOTES:
- These settings assume that there is no external authentication enabled

##
1) Set initial IP configurations to SDX
2) Also enable Applicance Supportability IP / XenServer IP if needed

```
set timezone timezone="UTC+0300 EEST Europe/Helsinki"
set hostname hostname=HOSTNAMEHERE
set systemsettings svm_ns_comm=https
set systemsettings secure_access_only=true
set systemsettings enable_session_timeout=true session_timeout=15 session_timeout_unit=Minutes
set systemsettings enable_shell_access=false
set systemsettings basicauth=false
set systemsettings enable_shell_access=false
set systemsettings enable_cuxip=false
set backuppolicy backup_to_retain=5
set passwordpolicy enable_password_complexity=true minimum_password_length=15
set userlockoutpolicy enable_user_lockout=true invalid_logins=5 user_lockout_interval=30
set systemuser id=USETABTOFILL password=YOURSECUREPASSWORD # NOTE: 'show systemuser' to get 'id' if other than 'nsroot' exists

add systemuser name=YOURALTERNATIVESUPERUSER password=YOURSECUREPASSWORD issuperuser=true groups=[owner]
add ntpserver server=x.x.x.x minpoll=6 maxpoll=10 key_id=0 autokey=false
add snmptrap dest_server=x.x.x.x dest_port=162 community=yourcommunitystring version=v2 / v3
add snmpmanager snmp_manager=x.x.x.x netmask=x.x.x.x community=yourcommunitystring
add nsadminprofile name=YOURNSPROFILENAME username=nsroot password=YOURSECUREPASSWORD use_global_setting_for_communication_with_ns=true svm_ns_comm=https
add syslogserver name=SYSLOGSERVERNAME ip_address=SYSLOGSERVERIP log_level_all=true port=514
```

## Other nice to have
```
set cliprompt promptString=YOURSDXHOSTNAME
```

## Explanations

```
# Timezone
set timezone timezone="UTC+0300 EEST Europe/Helsinki"

# Hostname
set hostname hostname=HOSTNAMEHERE

# Secure Access Only
set systemsettings secure_access_only=true

# HTTPS Communication with Citrix ADC Instance
set systemsettings svm_ns_comm=https

# Enable Session Timeout, Session Timeout 15 min, Session Timeout Unit in Minutes
set systemsettings enable_session_timeout=true session_timeout=15 session_timeout_unit=Minutes

# Disable shell access from non-root users
set systemsettings enable_shell_access=false

# Do not Allow Basic Authentication
set systemsettings basicauth=false

# Do not enable Shell access for non-nsroot User
set systemsettings enable_shell_access=false

# Disable CUXIP User Experience Improvement Settings/telemetry
set systemsettings enable_cuxip=false

# Retain more than default 3 backups
set backuppolicy backup_to_retain=5

# Set 'Enable Password Complexity' and 'Minimum Password Length' password policy. Reference (NIST) Special Publication 800-63B / single-factor authentication 
set passwordpolicy enable_password_complexity=true minimum_password_length=15

# Set user lockout policy
set userlockoutpolicy enable_user_lockout=true invalid_logins=5 user_lockout_interval=30

# Change 'nsroot' user default password
set systemuser id=USETABTOFILL password=YOURSECUREPASSWORD # NOTE: 'show systemuser' to get 'id' if other than 'nsroot' exists

# Add alternative superuser account as best practise and use it instead of 'nsroot'
add systemuser name=YOURALTERNATIVESUPERUSER password=YOURSECUREPASSWORD issuperuser=true groups=[owner]

# Add your NTP server
add ntpserver server=x.x.x.x minpoll=6 maxpoll=10 key_id=0 autokey=false

# Add SNMP traps
add snmptrap dest_server=x.x.x.x dest_port=162 community=yourcommunitystring version=v2 / v3

# Add SNMP managers
add snmpmanager snmp_manager=x.x.x.x netmask=x.x.x.x community=yourcommunitystring

# Add nsadminprofile
add nsadminprofile name=YOURNSPROFILENAME username=nsroot password=YOURSECUREPASSWORD use_global_setting_for_communication_with_ns=true svm_ns_comm=https

# Add syslog server
add syslogserver name=SYSLOGSERVERNAME ip_address=SYSLOGSERVERIP log_level_all=true port=514
```
