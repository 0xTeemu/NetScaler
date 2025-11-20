# Basic VPX settings for new applicance 

```
enable ns mode FR L3 Edge USNIP PMTUD
disable feature callHome
set ns tcpParam -WS ENABLED -SACK ENABLED 
set system user nsroot -externalAuth DISABLED
set ns param -cookieversion 1 -secureCookie ENABLED
set ns httpParam -dropInvalReqs ON
set snmp alarm CPU-USAGE -thresholdValue 80 -normalValue 30 -state ENABLED -severity Informational -logging ENABLED
set snmp alarm MEMORY -thresholdValue 80 -normalValue 30 -state ENABLED -severity Critical -logging ENABLED
set system parameter -strongpassword enablelocal -minpasswordlen 9
set ns ip x.x.x.x -restrictAccess enabled
set ica parameter -EnableSRonHAFailover YES -force 
set ssl parameter defaultProfile ENABLED -force
set ssl parameter -denySSLReneg NONSECURE
set ns param -timezone "GMT+02:00-EET-Europe/Helsinki"
set ns ip x.x.x.x -ftp DISABLED -telnet DISABLED -gui SECUREONLY
set HA node -failSafe ON
set aaa parameter -maxLoginAttempts 3 -failedLoginTimeout 15 -persistentLoginAttempts ENABLED
set ssl parameter -sendCloseNotify y
set vpn parameter -defaultAuthorizationAction DENY
set aaa parameter -loginEncryption ENABLED 
set ns param -cip ENABLED X-Forwarded-For
```
