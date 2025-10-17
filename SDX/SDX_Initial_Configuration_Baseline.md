# Intial configurations to new SDX

##
1) Set initial IP configurations to SDX
2) Also enable Applicance Supportability IP / XenServer IP if needed

```
set timezone timezone="UTC+0300 EEST Europe/Helsinki"
set hostname hostname=HOSTNAMEHERE
set systemsettings svm_ns_comm=https
set systemsettings secure_access_only=true
set systemsettings enable_session_timeout=true session_timeout=15 session_timeout_unit=Minutes
set systemsettings basicauth=false
set systemsettings enable_shell_access=false
set systemsettings enable_cuxip=false
set backuppolicy backup_to_retain=5
set systemuser id=USETABTOFILL password=YOURSECUREPASSWORD # NOTE: 'show systemuser' to get 'id' if other than 'nsroot' exists

add systemuser name=YOURALTERNATIVESUPERUSER password=YOURSECUREPASSWORD issuperuser=true
add ntpserver server=x.x.x.x minpoll=6 maxpoll=10 key_id=0 autokey=false
add snmptrap dest_server=x.x.x.x dest_port=162 community=yourcommunitystring version=v2 / v3
add snmpmanager snmp_manager=x.x.x.x netmask=x.x.x.x community=yourcommunitystring
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

# Do not Allow Basic Authentication
set systemsettings basicauth=false

# Do not enable Shell access for non-nsroot User
set systemsettings enable_shell_access=false

# Disable CUXIP User Experience Improvement Settings/telemetry
set systemsettings enable_cuxip=false

# Retain more than default 3 backups
set backuppolicy backup_to_retain=5

# Change 'nsroot' user default password
set systemuser id=USETABTOFILL password=YOURSECUREPASSWORD # NOTE: 'show systemuser' to get 'id' if other than 'nsroot' exists

# Add alternative superuser account as best practise and use it instead of 'nsroot'
add systemuser name=YOURALTERNATIVESUPERUSER password=YOURSECUREPASSWORD issuperuser=true

# Add your NTP server
add ntpserver server=x.x.x.x minpoll=6 maxpoll=10 key_id=0 autokey=false

# Add SNMP traps
add snmptrap dest_server=x.x.x.x dest_port=162 community=yourcommunitystring version=v2 / v3

# Add SNMP managers
add snmpmanager snmp_manager=x.x.x.x netmask=x.x.x.x community=yourcommunitystring
```
