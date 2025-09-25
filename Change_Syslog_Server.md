# Workflow to Replace Syslog Configuration on NetScaler
## Instructions

**Pre-requirements:** Old syslog policy is Advanced Global Policy Binding. This doesn't work with Classic Global Policy Bindings without modifying the commands.
1) Go to shell
```
shell
```
3) Save running configs
nscli -U 127.0.0.1:nsroot:yourpassword "save ns config"

4) Make backup from current ns.conf file
cp /nsconfig/ns.conf /nsconfig/ns.conf_backup

5) Remove syslogGlobal binding:
for globalbind in $(nscli -U 127.0.0.1:nsroot:yourpassword "show audit syslogGlobal" | awk '{for (i=1;i<=NF;i++) if ($i=="Name:") print $(i+1)}'); do nscli -U 127.0.0.1:nsroot:yourpassword "unbind audit syslogGlobal $globalbind"; done

6) Remove all syslogPolicies
for pol in $(nscli -U 127.0.0.1:nsroot:yourpassword "show audit syslogPolicy" | awk '{for (i=1;i<=NF;i++) if ($i=="Name:") print $(i+1)}'); do nscli -U 127.0.0.1:nsroot:yourpassword "rm audit syslogPolicy $pol"; done

7) Remove all syslogActions
for act in $(nscli -U 127.0.0.1:nsroot:yourpassword "show audit syslogAction" | awk '{for (i=1;i<=NF;i++) if ($i=="Name:") print $(i+1)}'); do nscli -U 127.0.0.1:nsroot:yourpassword "rm audit syslogAction $act"; done

8) Add new syslogAction
nscli -U 127.0.0.1:nsroot:yourpassword "add audit syslogAction your_syslog_action 213.138.150.236 -logLevel ALL -acl ENABLED -userDefinedAuditlog YES"

9) Add new syslogPolicy
nscli -U 127.0.0.1:nsroot:yourpassword "add audit syslogPolicy your_syslog_policy true your_syslog_action"

10) Bind globally
nscli -U 127.0.0.1:nsroot:yourpassword "bind audit syslogGlobal -policyName your_syslog_policy -priority 100"

11) Save running configs
nscli -U 127.0.0.1:nsroot:yourpassword "save ns config"

```
shell
nscli -U 127.0.0.1:nsroot:yourpassword "save ns config"
cp /nsconfig/ns.conf /nsconfig/ns.conf_backup
for globalbind in $(nscli -U 127.0.0.1:nsroot:yourpassword "show audit syslogGlobal" | awk '{for (i=1;i<=NF;i++) if ($i=="Name:") print $(i+1)}'); do nscli -U 127.0.0.1:nsroot:yourpassword "unbind audit syslogGlobal $globalbind"; done
for pol in $(nscli -U 127.0.0.1:nsroot:yourpassword "show audit syslogPolicy" | awk '{for (i=1;i<=NF;i++) if ($i=="Name:") print $(i+1)}'); do nscli -U 127.0.0.1:nsroot:yourpassword "rm audit syslogPolicy $pol"; done
for act in $(nscli -U 127.0.0.1:nsroot:yourpassword "show audit syslogAction" | awk '{for (i=1;i<=NF;i++) if ($i=="Name:") print $(i+1)}'); do nscli -U 127.0.0.1:nsroot:yourpassword "rm audit syslogAction $act"; done
nscli -U 127.0.0.1:nsroot:yourpassword "add audit syslogAction your_syslog_action 213.138.150.236 -logLevel ALL -acl ENABLED -userDefinedAuditlog YES"
nscli -U 127.0.0.1:nsroot:yourpassword "add audit syslogPolicy your_syslog_policy true your_syslog_action"
nscli -U 127.0.0.1:nsroot:yourpassword "bind audit syslogGlobal -policyName your_syslog_policy -priority 100"
nscli -U 127.0.0.1:nsroot:yourpassword "save ns config"
```
